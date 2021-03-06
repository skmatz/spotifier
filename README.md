# Spotifier

[![pypi](https://img.shields.io/pypi/v/spotifier)](https://pypi.org/project/spotifier)
[![build](https://img.shields.io/github/workflow/status/skmatz/spotifier/build)](https://github.com/skmatz/spotifier/actions?query=workflow%3Abuild)
[![release](https://img.shields.io/github/workflow/status/skmatz/spotifier/release?label=release)](https://github.com/skmatz/spotifier/actions?query=workflow%3Arelease)
[![python version](https://img.shields.io/pypi/pyversions/spotifier)](https://pypi.org/project/spotifier)
[![license](https://img.shields.io/github/license/skmatz/spotifier)](./LICENSE)

:notes: A Spotify Web API Library for Modern Python

## Notice

I do not recommend using this package as it is not yet ready for use.

## Feature

- All functions supports type hint (Up to the level of TypedDict!)
- Reproduce API documentation with code as much as possible (You can handle errors w/o wasting requests!)

## Install

### PyPI

```sh
pip install spotifier
```

### Source

```sh
pip install git+https://github.com/skmatz/spotifier.git
```

## Quick Start

```python
import os
import webbrowser  # to open URL in browser

from spotifier import Spotify
from spotifier.oauth import SpotifyAuthorizationCode


oauth = SpotifyAuthorizationCode(
    client_id=os.environ["SPOTIFY_CLIENT_ID"],
    client_secret=os.environ["SPOTIFY_CLIENT_SECRET"],
    redirect_uri=os.environ["SPOTIFY_REDIRECT_URI"],
)

webbrowser.open(oauth.get_authorize_url())
url = input("Input redirected URL: ")

code = oauth.parse_response_code(url)
oauth.set_token(code)

client = Spotify(oauth)

print(client.get_current_users_profile()["display_name"])  # your Spotify nickname
```

## Supported API

- [x] Authorization Code Flow
- [ ] Client Credentials Flow
