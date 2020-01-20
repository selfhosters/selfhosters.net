# [Selfhosters.net](https://selfhosters.net/)

[![Unraid](https://raw.githubusercontent.com/selfhosters/unRAID-CA-templates/master/.github/ISSUE_TEMPLATE/discord_unraid_unraid.png )](https://discord.gg/qWPbc8R)

[![Discord](https://img.shields.io/discord/641230698166091777?color=%23ff8c2f&label=Discord&logo=discord&logoColor=%23ff8c2f&style=for-the-badge)](https://discord.gg/qWPbc8R)
[![GitHub contributors](https://img.shields.io/github/contributors/selfhosters/selfhosters.net.svg?color=%23ff8c2f&style=for-the-badge)](https://github.com/selfhosters/selfhosters.net/graphs/contributors)

Repository for the selfhosters.net documentation.

## Start documenting

Create or edit a markdown(.md) file in the [/docs](/docs/) folder.

It's based on markdown, so looking at a [cheat sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatshee), and checking changes against a [live preview](https://markdownlivepreview.com/) helps you confirm the changes appear like you want them to.

## Start documenting (and seeing changes live)

### Clone repository

```bash
git clone https://github.com/selfhosters/selfhosters.net.git
cd selfhosters.net/
```

### Create and activate python virtual environment ([docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/))

```bash
python3 -m venv ./venv
source venv/bin/activate
```

### Install required packages

```bash
pip install -r requirements.txt
```

### Start the dev-server

```bash
mkdocs server
```

### Write your documentation

### Commit your changes
