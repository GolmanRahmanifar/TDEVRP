# TDEVRP benchmark instances

Benchmark instances for the time-dependent electric vehicle routing problem with time windows used in the study *Temporal Granularity and Recharging Policies in Time-Dependent Electric Vehicle Routing for Urban Logistics*.

The benchmark contains 49 synthetic urban instances with 5 to 50 customers in seven operating classes.

## Contents

| Folder | Instances | Customers |
|---|---|---|
| `instances/small/` | 13 | 5, 10 |
| `instances/medium/` | 21 | 15, 20, 25 |
| `instances/large/` | 15 | 30, 40, 50 |

`instances/manifest.csv` lists every instance with its size class, operating class, number of customers, vehicles and charging stations, and generator seed.

## Naming

`<size>_<class>_n<customers>_v<vehicles>_rs<stations>.json`

For example, `M_tim_n015_v02_rs03` is a medium time-window instance with 15 customers, 2 vehicles and 3 charging stations. Class codes: `std` standard, `cap` capacity, `cng` congestion, `eng` energy, `geo` geographic, `mix` mixed, `tim` time-window.

## File format

Each instance is a JSON file with the following fields.

- `metadata`: instance name, size class, operating class (`stress_type`), counts, generator seed and design information.
- `depot`, `customers`, `charging_stations`, `vehicles`: coordinates in km on a 24 km x 24 km area with the depot at the centre; customer demand in kg; time windows and service times in minutes from midnight; charging rate in kWh/min; vehicle payload capacity in kg and battery capacity in kWh; `initial_soc` as a fraction of battery capacity.
- `distance_matrix`: Euclidean distances in km. Nodes are ordered as depot, customers, then charging stations.
- `time_matrices`: travel times in minutes. `static` gives one value per arc; `level_3`, `level_5` and `level_7` give one value per departure interval of the three-, five- and seven-period planning profiles; `level_96` gives one value per 15-minute interval of the reference profile.
- `traffic`: base speed (50 km/h), interval breakpoints and zone speed factors for the planning profiles and the 15-minute reference profile.

Customer time windows open no earlier than 06:00 (360 min) and close no later than 20:00 (1200 min).

The vehicle field `consumption_rate` is not used in the study. Energy consumption is computed from travel time and distance, with 0.033 kWh/min and 0.30 kWh/km in the baseline setting.
