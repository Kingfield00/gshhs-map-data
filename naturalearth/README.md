# Natural Earth 5.0.0: rivers in tiles for MapForge

The rivers and lakes' centre lines of Natural Earth at 1:10 million (ne_10m_rivers_lake_centerlines, version 5.0.0), cut into tiles of 5° for MapForge, which follows them when it works out a map's rivers from its heights on flat land.

- Tiles: 621; lines: 1473; 1.3 MB in all.
- Each tile, ".mfnr": "MFNR", the format, its column from 180° W and its row from 90° S, then deflated: the lines, each its scale rank (1 the most important), its name and its points as differences of millionths of a degree.
- The changes: the lines cut at the tiles' edges; only the scale rank and the name of each kept.

Source: Natural Earth, https://www.naturalearthdata.com. Made with Natural Earth. Free vector and raster map data @ naturalearthdata.com.
