# OSM Liberty [![BSD licensed](https://img.shields.io/badge/license-BSD-blue.svg)](https://github.com/maputnik/osm-liberty/blob/gh-pages/LICENSE.md) [![GitHub CI status](https://github.com/maputnik/osm-liberty/workflows/CI/badge.svg)](https://github.com/maputnik/osm-liberty/actions?query=workflow%3ACI)

<img align="right" alt="OSM Liberty" src="logo.png" />

A free Mapbox GL basemap style for everyone with complete liberty to use and self host. OSM Liberty is a fork of OSM Bright based on free data sources with a mission for a clear good looking design for the everyday user. It is based on the vector tile schema of [OpenMapTiles](https://github.com/openmaptiles/openmaptiles).

**[Preview OSM Liberty with Maputnik](https://maputnik.github.io/editor/?style=https://trailstash.github.io/osm-liberty/style.json)**

## Usage

You can use the style in your Mapbox GL maps.

By default, the vector tiles are served from [OSM Americana Community Vector Tile Server](https://tile.ourmap.us/) and the
[raster tiles](https://github.com/TrailStash/naturalearthtiles) and [sprites](https://github.com/TrailStash/osm-liberty/tree/gh-pages/sprites)
and [glyphs](https://github.com/TrailStash/openmaptiles-fonts) directly from GitHub.

Another option is to create your own vector tiles with [OpenMapTiles](https://github.com/openmaptiles/openmaptiles) and host the tiles and assets yourself for complete liberty.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset=utf-8 />
  <title>OSM Liberty</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <style>
    body { margin:0; padding:0; }
    #map { position:absolute; top:0; bottom:0; width:100%; }
  </style>
  <script src='https://api.mapbox.com/mapbox-gl-js/v1.10.1/mapbox-gl.js'></script>
  <link href='https://api.mapbox.com/mapbox-gl-js/v1.10.1/mapbox-gl.css' rel='stylesheet' />
</head>
<body>
  <div id='map'></div>
  <script>
  var map = new mapboxgl.Map({
      container: 'map',
      style: 'https://maputnik.github.io/osm-liberty/style.json',
      center: [8.538961,47.372476],
      zoom: 5,
      hash: true
  });
  </script>
</body>
</html>
```

## Data Sources

- [OpenMapTiles](http://openmaptiles.org/) as vector data source
- [Natural Earth Tiles](https://klokantech.github.io/naturalearthtiles/) for relief shading
- [Maki](https://www.mapbox.com/maki-icons/) as icon set

## Map Design

The map design originates from OSM Bright but strives to reach a unobtrusive and clean design for everyday use.
Colored relief shading from Natural Earth make the low zoom levels look good.

[![OSM Liberty Map demo](demo/zoom.gif)](https://maputnik.github.io/osm-liberty/)

## Edit the Style

You can [edit the style directly online in Maputnik](https://maputnik.github.io/editor?style=https://maputnik.github.io/osm-liberty/style.json).

This style actually triggered the need for the development of [Maputnik](https://github.com/maputnik/editor/).

A pre-commit hook is included to validate and format the JSON styles using
[`mapbox-gl-style-spec`](https://www.npmjs.com/package/@mapbox/mapbox-gl-style-spec).
To use, just install the NPM dev dependencies:
```
npm install
```
and then validate or format the style with
```
npm run validate
npm run format
```

Validation and reformatting will happen automatically on commit if you have the
dependencies installed.

## Icon Design

A [Maki](https://github.com/mapbox/maki) icon set using colors to distinguish between icon categories.

Maki is a living project and adds new icons over time, which means that there
could be new icons that OSM Liberty could use for POIs. `maki_list.py` is a
simple script to list both the names in OSM Liberty's iconset that don't map to
any valid Maki name, and the Maki names that are not currently used in OSM
Liberty's iconset. You can run the script with `python3 maki_list.py`.

**Color Palette**

Color Name   | Hex Value
-------------|----------
Blue         | `#5d60be`
Light Blue   | `#4898ff`
Orange       | `#d97200`
Red          | `#ba3827`
Brown        | `#725a50`
Green        | `#76a723`

**Modify Icons**

_When submitting a PR, no need to include the sprites. They will be automatically created when merging a PR.<br>
The size 11 icons are included in the sprites for backward compatability. Please don't include new size 11 icons._

1. Take the `iconset.json` and import it to the [Maki Editor](https://www.mapbox.com/maki-icons/editor/).
2. Apply your changes and download the icons in SVG format and the iconset in JSON format.
Save the downloaded SVGs from Maki Editor to the folder [svgs_iconset](https://github.com/maputnik/osm-liberty/tree/gh-pages/svgs/svgs_iconset).
3. Mandatory if the updated `iconset.json` should become part of this repo: Format the JSON with `cat iconset.json | jq -MS '.'` for better legibility.
4. There are also SVGs in the folder [svgs_not_in_iconset](https://github.com/maputnik/osm-liberty/tree/gh-pages/svgs/svgs_not_in_iconset).
These are the SVGs for road shields, the dot used for city and town layers and the road area pattern which could not be modified using the Maki Editor. To modify these you could use e.g. [Inkscape](https://inkscape.org).
5. Install the NPM dev dependencies: `npm install` to have [spritezero-cli](https://gitlab.com/beyondtracks/spritezero-cli) available (we're using a fork of https://github.com/mapbox/spritezero-cli ).
6. Generate the low and high resolution sprites: `npm run build_sprites`

## Have a look at ...

- [OSM Liberty Topo](https://github.com/nst-guide/osm-liberty-topo) - a topographic fork of OSM Liberty
- [TrailStash Liberty](https://gitlab.com/trailstash/liberty) - a fork of OSM Liberty Topo
