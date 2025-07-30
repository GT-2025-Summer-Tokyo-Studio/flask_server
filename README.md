# flask_server (Backend)

## Purpose: Hosts the Flask API server that processes:
  - Address inputs
  - Nearby shelter search
  - Heat-aware route computation

### Key files:
  - app.py: Flask app entry point
  - heat_route_planner_v2.py: Core routing logic
  - shelters.py, routes.py: Data utilities
  - requirements.txt: Backend dependencies


---

- **`heat_route_planner_v2.py`**   – Backend Routing Engine for Flask App

This version of the heat-aware routing engine is built for **integration with a Flask server**. It does not run in the terminal, but instead exposes functionality that can be triggered from a **web app or dashboard** via API calls.



### 🔧 Purpose

- Serve as the **backend engine** that:
  - Accepts origin coordinates (latitude, longitude) from user input
  - Identifies the 5 nearest evacuation shelters
  - Predicts current **heat scenario** using real-time weather
  - Computes:
    - 🥵 Heat-optimized walking route
    - 🚶 Shortest walking route
    - 🚗 Driving route
  - Returns key stats: time, distance, risk, vulnerability
  - Generates route geometries for frontend map display


### 🧩 Typical Usage

This script is **imported and called inside `app.py`**, the Flask server. It enables:

- API endpoint like `/get_route?origin=...&destination=...`
- Output in JSON or GeoJSON format
- Route stats used for user-side dashboards

### 🗂️ Input & Output

- **Input:** Address name from user-selected origin and shelter number
- **Output:** 
  - GeoJSON of route segments (walking + driving)
  - Summary stats: time, distance, heat risk, water needed
  - Vulnerability labels for each segment
 

## 🌐 Run Code and Output of `app.py` in Terminal
1. Change directory to the script folder.
   ```bash
   cd path/to/UHE_classifier

2. Run the server:

    ```bash
    python app.py

3. Once started, the Flask app will be running at:
http://127.0.0.1:8083/get-test

## Example API Calls
  🏠 Query Nearby Shelters
  Get the 5 closest shelters to a location (e.g., Nihonbashi Station):

  - http://127.0.0.1:8083/query-shelters?address=nihonbashi%20station
  - 📤 Output: JSON response with shelter names, capacities, and distances.

🧭 Query Optimized Route to Selected Shelter
  Compute routes from the given address to one of the suggested shelters:

  - http://127.0.0.1:8083/query-routes?address=nihonbashi%20station&shelter_id=1
  - 📤 Output: GeoJSON with:
    - Heat-optimized walking path
    - Driving route
    - Route segment stats (heat risk, distance, vulnerability)









