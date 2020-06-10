# How to Put unRAID containers on their own VLAN inside a VPN Tunnel using PFSense

!!! example "Credits:"

    Written by Schwiing#3404

    Based on the work of IamSpartacus#3678

Disclaimer: This guide makes the following assumptions:

* You're using PFsense as your Firewall

* You're using unRAID

* You have a VPN Provider (In this example I used mullvad)

* You have a managed switch and know how to tag VLAN traffic on that switch (In this example I used unifi)

--------

## Create OpenVPN Clients in PFSense

1. Head to VPN -> OpenVPN -> Clients -> + Add

2. Fill out the client information based on your provider. I use mullvad, so I followed this guide: [mullvad.net](https://mullvad.net/en/help/using-pfsense-mullvad/)

3. The only differences I made were:

    a. Set Server Host to: (a server closer to you  from this [list](https://mullvad.net/servers))

    b. Make sure these are checked:

       * Bars the server from adding routed to the client's routing table

       * Don't add or remove routes automatically

4. Mullvad supports up to 5 connections at once. So if you want to go down that route, add 5 clients

    a. Make sure to add a different server host for each client

--------

## Add interface assignments for each OpenVPN Client

1. This is just a matter of creating an interface for each new ovpnc* you made earlier

2. Interfaces -> Assignments -> + Add. I named them based on the server each interface would connect to

3. For example, my first interface name is MULLVAD_CHICAGO_002 (same as the server it connects to)

4. Create the rest of your interfaces (remember, up to 5)

### Create a VLAN

1. Interfaces -> VLANs -> + add

2. Select your LAN as your parent interface (Physical NIC)

3. Pick a VLAN Tag. Make sure you remember this for later. I picked "90", so my network is 192.168.90.0/24

4. Add a description. I used "DOCKER_VPN"

### Create NAT Mappings

1. Firewall -> NAT -> Outbound

2. Make sure Outbound NAT Mode = Manual

3. Add a rule to the top of the list with the following settings:
    * Interface: MULLVAD_CHICAGO_002
    * Protocol: Any
    * Source: Network, 192.168.90.0/24 (Fill in whatever your VLAN Tag + Network is here)

### Create Gateway Group

1. System -> Routing -> Gateway Groups -> + Add

2. Set all of your new gateways to Tier 1

3. Trigger Level: Packet Loss or High Latency

4. Keep WAN_DHCP at "Never" Tier

5. Name it. I called it "Mullvad Gateway Group"

--------

## Create VLAN Rule

1. Select your new VLAN (Mine is DOCKER_VPN)

2. Top Rule:
    * Action: Pass
    * Interface: DOCKER_VPN
    * Address Family: IPv4
    * Source: DOCKER_VPN net
    * Destination: LAN net

3. Bottom Rule:
    * Hit "Display Advanced" under Extra Options
    * Action: Pass
    * Interface: DOCKER_VPN
    * Address Family: IPv4
    * Source: DOCKER_VPN net
    * Destination: any
    * Gateway: Mullvad_VPN_Group

### Add DNS Servers to VLAN

1. Services -> DHCP Server -> DOCKER_VPN

2. DNS Servers (these are for mullvad. YMMV):
    * 193.138.218.74
    * 10.8.0.1

## Misc PFsense Steps

1. System -> Advanced -> Miscellaneous

2. Gateway Monitoring: Do not create rules when gateway is down -> CHECKED

--------

## unRAID steps

1. Go to Network settings
    * Enable VLANs: Yes
    * VLAN Number: 90 (whatever you set your VLAN Tag earlier in Pfsense)
    * Network Protocol: Ipv4 Only
    * IPv4 Address: 192.168.90.31 (whatever you want here, under the same subnet)
    * IPv4 default gateway: 192.168.90.1

2. Next, Docker settings. Enable Docker: No, Advanced view: on
    * Host Access to custom networks: Enabled
    * Ipv4 custom network on interface br0.90:
        * Subnet: 192.168.90.0/24
        * Gateway: 192.168.90.1
        * DHCP Pool: 192.168.90.240/28 (16 hosts) [Set whatever you want here. 16 was plenty for me]

3. Once done, you now have a new VLAN in Unraid.

4. Assign docker container new network. Set a static IP if it's easier for your Reverse Proxied containers
