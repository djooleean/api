---
title: "Expander"
---

### Expander

## What?

The expander feature is used to combine multiple requests. For example, a game provides a list of company IDs which in turn need to be requested to reach the company data. Using the expander parameter, the company ID will instead be an object containing that data.

## Where?

The expander can be used on any entity that has sub-properties such as Games, Companies, People etc.

## How?

**Example**: `/games/1838,828,1337?fields=name,themes.name,game.name&expand=game,themes`

We start with this simple URL.

`/games/1838,828,1337`
First we have the resource part of the url. In this case we get the games with ID: 1838, 828 and 1337

`expand=game,themes`
With this parameter, we will expand: game (parent game) and themes (the themes that the game has).

`fields=name,themes.name,game.name`
We also have to specify all the fields we want to have expanded. If you don't specify the fields it will give you the full object.

* name: The field on the root game model.
* game.name: The field on the parent game model.
* themes.name: The field on the theme model.

The result will be:
```json

[
  {
    "id": 1838,
    "name": "Painkiller: Redemption",
    "game": {
      "id": 828,
      "name": "Painkiller"
    },
    "themes": [
      {
        "id": 1,
        "name": "Action"
      },
      {
        "id": 19,
        "name": "Horror"
      }
    ]
  }
]

```
Now for the more advanced expander:

`/pulses/19357?fields=title,pulse_source.name,pulse_source.page.name,pulse_source.page.logo&expand=pulse_source.page`

We get the pulse news article with ID: 19357.

`expand=pulse_source.page`
We want the pulse_source and it's page with associated logo's and deeper information.

`fields=title,pulse_source.name,pulse_source.page.name,pulse_source.page.logo`
Because the pulse_source is inferred, you can also specify fields on the pulse_source as well.

The result is:
```json
[
  {
    "id": 19357,
    "title": "Today’s selection of articles from Kotaku’s reader-run community: Anatomy of a Fire Emblem Character",
    "pulse_source": {
      "id": 1,
      "name": "Kotaku",
      "page": {
        "id": 501,
        "name": "Kotaku",
        "logo": {
          "url": "//images.igdb.com/igdb/image/upload/t_thumb/ns8o3b99iwdbyee8wu9c.png",
          "cloudinary_id": "ns8o3b99iwdbyee8wu9c",
          "width": 240,
          "height": 240
        }
      }
    }
  }
]
```

## What can I expand?

- `Game.collection`
- `Game.franchise`
- `Game.franchises`
- `Game.game`
- `Game.games`
- `Game.developers`
- `Game.publishers`
- `Game.game_engines`
- `Game.player_perspectives`
- `Game.game_modes`
- `Game.keywords`
- `Game.themes`
- `Game.genres`
- `Character.games`
- `Company.published`
- `Company.developed`
- `GameEngine.games`
- `GameEngine.platforms`
- `GameEngine.companies`
- `GameMode.games`
- `Keyword.games`
- `PulseSource.game`
- `PulseSource.page`
- `Theme.games`
- `Collection.games`
- `PlayerPerspective.games`
- `Franchise.games`
- `Genre.games`
- `ReleaseDate.game`
- `ReleaseDate.platform`
- `Page.feed`
- `Page.game`
- `Pulse.pulse_source`
- `Review.game`
- `Person.games`
- `Person.characters`
- `Feed.games`
- `Feed.pulse`
- `PulseGroup.game`
- `PulseGroup.pulses`
