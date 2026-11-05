# Delivery routing in Neuquén · VRP with time windows

**[Open the interactive demo](https://juanlaigle-hub.github.io/vrp-neuquen/)** · [Español](#español)

A food distributor delivers from its warehouse to 48 shops across Neuquén, Argentina, with 5 trucks of 220 boxes each. Every shop has a morning (08–12), afternoon (14–18) or all-day delivery window. The demo compares three situations on a map:

| Scenario | km driven | Late deliveries | Shops served |
|---|---|---|---|
| **1. Manual plan:** the city split into 5 zones around the warehouse, nearest shop first | 124.1 | 16 | 48 |
| **2. Optimized:** capacitated VRP with time windows solved with Google OR-Tools | **97.1 (−22 %)** | **0** | 48 |
| **3. Truck breakdown at 10:30:** re-planned from each truck's current position | 101.3 | 0 | 48 (5 would be lost without re-routing) |

The manual plan also leaves one truck overloaded (225 boxes for 220).

## Model

- **CVRPTW:** vehicle capacity, hard time windows, service time per stop (6 min + 0.15 min per box), shift 07:30–18:30.
- **Solver:** OR-Tools routing library, cheapest-arc first solution and guided local search.
- **Re-routing:** at the breakdown time, deliveries already made are fixed; the pending stops of all trucks plus the broken truck's orders are re-solved, with each truck starting from its last stop, its current clock and its remaining capacity.
- **Travel times:** grid-city distance (Manhattan × 1.08) at 24 km/h. In a real project this comes from a road network (OSRM or a maps API).

## About the data

Shops, orders and windows are simulated. On the map, routes are drawn along the streets with OSRM (OpenStreetMap data) over a CARTO base map; the optimization itself used grid-city distances.

The solver code is private. This repository contains the interactive page and the computed results. For a demo with your own data, write to [juanlaigle@gmail.com](mailto:juanlaigle@gmail.com).

## Español

Una distribuidora de alimentos reparte desde su depósito a 48 comercios de Neuquén con 5 camiones de 220 cajas y ventanas horarias. El plan optimizado con OR-Tools recorre **22 % menos km y no tiene entregas tarde** (el manual tiene 16). Cuando un camión se rompe a las 10:30, el sistema recalcula desde donde está cada camión y reparte sus 5 entregas pendientes entre los otros 4, sin entregas tarde. Datos simulados.

---

[Juan Laiglecia](https://www.linkedin.com/in/juanlaiglecia) · [Ingeniería VR](https://www.ingenieriavr.com) · © All rights reserved. Map library: [Leaflet](https://leafletjs.com) (BSD-2-Clause), map data © OpenStreetMap contributors.
