# LEO Satellite Orbital Characteristics and V2X Communication Dataset (Ancona)

This repository contains the high-fidelity Low Earth Orbit (LEO) satellite tracking and V2X communication link dataset used for evaluating dynamic serverless edge orchestration algorithms.

## Dataset Location
The dataset file is located in this repository at:
*   **[`realworld/hypatia/leo_sats_ancona_dataset.csv`](file:///home/rriggio/sumo/build/ns-3-workspace/V2X-Lyapunov/realworld/hypatia/leo_sats_ancona_dataset.csv)**

## Dataset Overview
The dataset (`leo_sats_ancona_dataset.csv`) contains simulated orbital mechanics, coordinates, Doppler shifts, and round-trip times (RTT) for LEO satellite passes. The data covers a continuous **1-hour ($3600\text{ s}$)** scenario at a **$1\text{ s}$ resolution**, mapped over the urban road network of Ancona, Italy (spatial bounding box of $1737\text{ m} \times 1039\text{ m}$).

At each second, the dataset tracks and records the details of the active overhead satellite offering the highest elevation angle (highest degree of coverage) relative to ground observers.

## Data Schema

The CSV file contains the following columns:

| Column Name | Unit | Description |
| :--- | :--- | :--- |
| `timestamp` | seconds | The elapsed simulation time step (from 0 to 3600). |
| `satellite_name` | - | Operational name of the active LEO satellite overhead. |
| `norad_id` | - | Unique five-digit NORAD catalog number of the satellite. |
| `elevation_deg` | degrees | Elevation angle of the satellite relative to ground observer coordinates. |
| `range_km` | km | Slant range (line-of-sight distance) from the ground center to the satellite. |
| `rtt_ms` | ms | Calculated round-trip time based on the slant range propagation delay. |
| `x_ecef_km` | km | X-coordinate of the satellite position in Earth-Centered, Earth-Fixed (ECEF) frame. |
| `y_ecef_km` | km | Y-coordinate of the satellite position in Earth-Centered, Earth-Fixed (ECEF) frame. |
| `z_ecef_km` | km | Z-coordinate of the satellite position in Earth-Centered, Earth-Fixed (ECEF) frame. |
| `vx_ecef_kms` | km/s | Velocity component of the satellite along the X-axis in the ECEF frame. |
| `vy_ecef_kms` | km/s | Velocity component of the satellite along the Y-axis in the ECEF frame. |
| `vz_ecef_kms` | km/s | Velocity component of the satellite along the Z-axis in the ECEF frame. |

## Usage and Integration

### Loading in Python
You can load and parse the dataset using `pandas`:
```python
import pandas as pd
df = pd.read_csv('realworld/hypatia/leo_sats_ancona_dataset.csv')
print(df.head())
```

### Simulators Integration
*   **Step-by-Step Read:** In each simulation time slot $t$, query the corresponding row where `timestamp == t`.
*   **Link Config:** Use the `rtt_ms` and `range_km` fields to configure the communication delay and path loss for your satellite net devices.
*   **Mobility Mapping:** The ECEF position and velocity vectors can be mapped to simulator mobility models (such as ns-3 or custom network simulators) to compute dynamic relative distances.

## Link to IEEE Dataport
This dataset is also hosted on [IEEE Dataport](https://dx.doi.org/10.21227/1wjs-ds49) for persistent referencing and citation.

## Funding Acknowledgment

This work was funded by the European Union under the Horizon Europe programme through the SNS JU (Grant Agreement No. 101192912, NexaSphere). Views expressed are those of the authors and do not necessarily reflect those of the EU or the SNS JU.
