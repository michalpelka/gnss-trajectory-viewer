# GNSS Trajectory Viewer

A tiny static, client-side web app for visualizing RTK GNSS trajectories from
`EXTRA_GNSS/*.nmea` logs, colored by GGA fix quality (RTK Fixed / RTK Float /
DGPS / GPS / Invalid).

**Live app:** https://michalpelka.github.io/gnss-trajectory-viewer/

## Usage

1. Open the live app (or `index.html` locally in any browser).
2. Drag & drop your `EXTRA_GNSS` folder (or a selection of `.nmea` files)
   onto the drop zone, or use "Choose folder".
3. The trajectory is drawn on an OpenStreetMap base layer, colored by fix
   quality, with a legend showing time spent per quality.

Everything runs locally in the browser — files are parsed client-side and
are **never uploaded anywhere**.

## How it works

Each line in a `.nmea` log looks like:

```
<capture_ts_ns> <recv_ts_ns> $GNGGA,hhmmss.ss,lat,N/S,lon,E/W,quality,numSV,HDOP,alt,...
```

The app parses `$GNGGA` sentences, converts NMEA `ddmm.mmmm` coordinates to
decimal degrees, and groups consecutive fixes by quality into colored
polyline segments.

## Local development

No build step — it's a single static `index.html` (Leaflet loaded from a
CDN). Just open the file in a browser, or serve the directory:

```
python3 -m http.server 8000
```

## Related

A Python CLI version that produces a standalone HTML report for a single
folder lives in the [HDMapping](https://github.com/MapsHD/HDMapping) repo at
`apps/console_tools/plot_gnss_trajectory.py`.
