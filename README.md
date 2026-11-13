# GSHHG 2.3.7 in tiles for MapForge

This repository holds the coastlines of GSHHG 2.3.7 cut into tiles of 5° × 5°, in the compact format MapForge reads. MapForge downloads only the tiles an area of the world needs, and checks each one against the fingerprint in its own copy of `index.json`.

- Tiles by resolution: c 1321, l 1420, i 1460, h 1471, f 1473.
- Total size: 36.0 MB.
- Levels: 1 land, 2 lakes, 3 islands in lakes, 4 ponds on them, 5 Antarctica's ice front (for the full resolution, the high resolution's, as its own has a flaw in its shape).

## The format

Each file `<resolution>/<column>_<row>.mfgs` covers the tile from longitude −180 + 5 × column and latitude −90 + 5 × row. It starts with `MFGS`, the format's version (1), the resolution and the column and row as two 16-bit numbers; the rest is DEFLATE. Inside: the number of rings, then for each ring its level, its number of points and the points in microdegrees, each as the difference from the point before (the first from the tile's south-west corner), zigzag-encoded in variable-length numbers. Each ring is cut to the tile, so that for a point inside the tile the parity of the pieces is that of GSHHG's whole polygons. Tiles of sea alone are not written.

The tiles are made from GSHHG's official shapefiles by `mapforge gshhg-pack`, with nothing done by hand.

## Source and licence

Coastline from GSHHG 2.3.7, the Global Self-consistent, Hierarchical, High-resolution Geography Database: Wessel, P., and W. H. F. Smith (1996), A global, self-consistent, hierarchical, high-resolution shoreline database, J. Geophys. Res., 101(B4), 8741-8743; archived as NOAA NCEI Accession 0304143, doi:10.25921/fe3s-bq64.

GSHHG is distributed under the GNU Lesser General Public License, version 3 or later: see `LICENSE.TXT` and `COPYING.LESSERv3`, from GSHHG's own distribution. These tiles are GSHHG's data in another format, under the same licence.

## The lakes

The folder `hydrolakes` holds the lakes of HydroLAKES in tiles of the same grid, under their own licence, CC BY 4.0: see `hydrolakes/README.md` and `hydrolakes/LICENSE.md`. From version 0.61 MapForge reads the coast from levels 1 and 5 only, and the lakes from there.

## The rivers

The folder `naturalearth` holds the rivers and lakes' centre lines of Natural Earth 5.0.0 at 1:10 million in tiles of the same grid, in the public domain: see `naturalearth/README.md` and `naturalearth/LICENSE.md`. From version 0.65 MapForge follows them when it works out a map's rivers from its heights. Made with Natural Earth. Free vector and raster map data @ naturalearthdata.com.
