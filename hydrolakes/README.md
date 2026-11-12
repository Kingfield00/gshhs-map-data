# HydroLAKES 1.0 in tiles for MapForge

This folder holds the lakes of HydroLAKES 1.0 cut into tiles of 5° × 5°, in the compact format MapForge reads: 936 tiles with 365837 lakes, 70.0 MB in all. MapForge downloads only the tiles an area of the world needs, and checks each one against the fingerprint in its own copy of `index.json`.

## The format

Each file `<column>_<row>.mfhl` covers the tile from longitude −180 + 5 × column and latitude −90 + 5 × row. It starts with `MFHL`, the format's version (1), and the column and row as two 16-bit numbers; the rest is DEFLATE. Inside, in variable-length numbers (signed ones zigzag-encoded): the number of lakes, and for each its identifier, its area in hundredths of km², its surface elevation in metres, its type (one byte), its name (its length in bytes, then UTF-8) and its pour point in microdegrees; then the number of rings, and for each the place of its lake in that table, its number of points and the points in microdegrees, each as the difference from the point before (the first from the tile's south-west corner). Each ring is cut to the tile, so that for a point inside the tile the parity of a lake's pieces, its islands included, is that of the whole lake. Tiles without lakes are not written.

The tiles are made from HydroLAKES's official shapefile by `mapforge hydrolakes-pack`, with nothing done by hand.

## Source

HydroLAKES, version 1.0, from https://www.hydrosheds.org/products/hydrolakes (the file HydroLAKES_polys_v10_shp.zip).

Messager, M.L., Lehner, B., Grill, G., Nedeva, I., Schmitt, O. (2016): Estimating the volume and age of water stored in global lakes using a geo-statistical approach. Nature Communications 7: 13603. doi:10.1038/ncomms13603

## Changes made

- Only the lakes of 0.5 km² or more are kept, and in them only the islands of 0.25 km² or more.
- Every ring is simplified with the Douglas–Peucker method to 0.0004° (about 45 m).
- The rings are cut to tiles of 5° × 5°. Each tile carries, for its lakes, the identifier, area, surface elevation, type, name and pour point of HydroLAKES.

## Licence

HydroLAKES is distributed under the Creative Commons Attribution 4.0 International licence (CC BY 4.0). These tiles are a changed version of it, under the same licence: see LICENSE.md.
