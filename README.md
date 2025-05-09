# Kano Health Facilities Web Map

## Project Overview

This project displays an interactive web map showcasing health facilities within the administrative wards of Kano, Nigeria. The map allows users to visualize the distribution of health facilities and see the number of facilities per ward. Wards are thematically colored based on the count of facilities they contain, and individual health facilities are styled by their operational level (Primary, Secondary, Tertiary).

**Live Demo:** https://adegbehingbegodwin.github.io/Health-Facilities-in-Kano/

## Features

*   **Interactive Map:** Built with Leaflet.js.
*   **Base Maps:** Choice between Google Streets and OpenStreetMap.
*   **Kano Wards Layer:**
    *   Displays administrative ward boundaries for Kano.
    *   Thematically colored based on the number of health facilities within each ward.
    *   Hovering over a ward highlights it and shows its name and facility count in an info box.
    *   Clicking on a ward zooms to its extent.
*   **Health Facilities Layer:**
    *   Displays individual health facility locations as points.
    *   Points are styled (color and size) based on their operational level (Primary, Secondary, Tertiary, Other/Unknown).
    *   Clicking on a facility point shows a popup with its name, level, and other available details.
    *   Facility marker size adjusts dynamically with map zoom level for better visibility.
*   **Layer Control:** Allows users to toggle base maps and overlay layers.
*   **Legends:**
    *   Separate legend for ward facility counts.
    *   Separate legend for health facility levels.
*   **Map Tools (from plugins):**
    *   Polyline Measure
    *   Mouse Position Coordinates
    *   Drawing/Editing (Leaflet-Geoman)
    *   Minimap
    *   Sidebar (if implemented)
    *   Easy Buttons (if used for custom actions)

## Data Sources

*   **Kano Wards:** `data/kano_wards_with_numpoints.geojson`
    *   This GeoJSON file contains the polygon geometries for Kano wards.
    *   It includes a `wardname` property for the ward's name.
    *   It critically includes a `NUMPOINTS` property, representing the count of health facilities within that ward. This property is used for thematic styling.
    *   *Data Source:(https://data.grid3.org/datasets/0824aded5f5a4d39b10871c667aa8ccf_0/explore?location=8.982545%2C8.685290%2C5.81)*
*   **Kano Health Facilities:** `data/kano_health_facilities.geojson`
    *   This GeoJSON file contains point geometries for health facilities.
    *   Key properties used:
        *   `facility_name`: Name of the health facility.
        *   `facility_Level`: Operational level (e.g., "Primary", "Secondary", "Tertiary"). Used for styling.

    *   *Data Source:(https://data.grid3.org/datasets/a0ed9627a8b240ff8b315a84575754a4_0/explore?location=8.978734%2C8.672086%2C5.81).*

## Technical Stack

*   **HTML5, CSS3, JavaScript (ES6+)**
*   **Leaflet.js:** Core mapping library.
*   **jQuery & jQuery UI:** For general DOM manipulation and UI components (if used beyond Leaflet).
*   **Leaflet Plugins:**
    *   `leaflet-ajax`: For asynchronously loading GeoJSON data.
    *   `L.Control.Sidebar`: For a collapsible sidebar (if implemented).
    *   `Leaflet.EasyButton`: For creating simple map control buttons.
    *   `Leaflet.PolylineMeasure`: For measuring distances and areas.
    *   `L.Control.MousePosition`: To display mouse coordinates.
    *   `Leaflet-Geoman`: For drawing and editing geometries on the map.
    *   `Control.MiniMap`: For an overview minimap.
*   **Bootstrap (v3.4.1):** For basic page styling and layout (used minimally around the map in the current version).
*   **Font Awesome:** For icons.
*   **Python with GeoPandas:** Used for pre-processing and filtering the GeoJSON data, specifically to calculate the `NUMPOINTS` attribute for the wards layer by performing a spatial join with the health facilities layer.

## Setup and Usage

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/AdegbehingbeGodwin/Health-Facilities-in-Kano/]
    cd [Health-Facilities-in-Kano]
    ```
2.  **Ensure Data Files:**
    *   Place `kano_wards_with_numpoints.geojson` and `kano_health_facilities.geojson` inside the `data/` subfolder.
    *   Ensure all Leaflet plugins (from the `plugins/` folder) and other local assets (like `style.css`, `source/jquery-ui.min.css`) are correctly placed as per the paths in `index.html`.
3.  **Run a Local Web Server:**
    Due to browser security restrictions (CORS policy) when loading local files via `XMLHttpRequest` (used by `leaflet-ajax`), you need to serve the `index.html` file through a local web server.
    *   **Using Python 3:**
        ```bash
        cd /path/to/your/project/directory
        python -m http.server
        ```
    *   **Using Python 2:**
        ```bash
        cd /path/to/your/project/directory
        python -m SimpleHTTPServer
        ```
    *   **Using VS Code Live Server:** If you have Visual Studio Code, install the "Live Server" extension, right-click `index.html`, and choose "Open with Live Server."
4.  **Open in Browser:**
    Navigate to `http://localhost:8000` (or the port specified by your server) in your web browser.
