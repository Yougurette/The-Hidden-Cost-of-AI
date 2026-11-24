# The Hidden Cost of AI

An interactive simulation that makes the physical infrastructure behind AI visible.
Drag data centres onto a map and watch what changes for the people who live there:
electricity, cooling water, power bills, noise, air and land.

The browser version is a prototype for a tabletop installation with projection mapping and physical cubes.

## Run it

No build step and no dependencies. Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

On GitHub: Settings → Pages → deploy from the `main` branch, root folder.

## Files

| File | What it is |
|---|---|
| `index.html` | The simulation: map, draggable data centres, effects and information panel |
| `map.html` | The base map on its own, without effects |

Everything (styles, map generation, effects) lives inside these two files. The map is generated
procedurally from a fixed seed, so it looks the same every time. Fonts load from Google Fonts.

## How it works

- **Map:** a fictional landscape (city, lake, river, outskirts, forests, farmland) drawn on a canvas in a cartographic style.
- **Data centres:** up to 5. Each one builds up over about 6 seconds. Moving or removing one leaves the cleared land behind.
- **Effects** (each follows its own spatial logic):

| Effect | Colour | How it spreads |
|---|---|---|
| Electricity / power bills | yellow → orange | the whole grid area; the city tints as bills rise |
| Water | blue | pipe from the nearest river or lake; water level drops, farmland dries (ochre) |
| Noise | orange | ripples around the site, dampened by forest |
| Air | grey | plume drifting east with the wind (from on-site generators) |
| Land | magenta | cleared area around each site, stays after removal |

- **Concentration:** data centres close together strengthen each other. From about 3, the grid is overloaded.

## Data status

| Marker | Meaning |
|---|---|
| `≈` | estimate from a published source |
| `◇` | model assumption made for this prototype |

| Figure | Value | Status | Source |
|---|---|---|---|
| Energy per text prompt | ≈ 0.3 Wh (0.1–0.6 Wh) | estimate | Ritchie 2026, IEA 2026 |
| Grid capacity of one hyperscale data centre | 100–150 MW | estimate | IEA |
| Cooling water, 100 MW, evaporative cooling | 0.5–2.5 million US gallons/day (≈ 1.9–9.5 million litres) | estimate | UC Riverside via The Register |
| AI-focused data centres, electricity 2025 | ≈ 155 TWh | estimate | IEA 2026 via Ritchie |
| All data centres, 2030 (base case) | ≈ 945 TWh | estimate | IEA 2026 via Ritchie |
| Share explained by text prompts | ≈ 2 % | estimate | Ritchie 2026 |
| Ireland, electricity to data centres (2023) | > 20 % | reported | CSO Ireland via Ritchie |
| Virginia, electricity to data centres (2023) | ≈ 25 % | reported | Virginia JLARC via Ritchie |
| Power bill increase, noise reach, air plume, water level drop | | model assumption | — |

Derived values (own arithmetic): 100 MW × 24 h = 2.4 GWh per day ≈ 8 billion prompts;
0.3 Wh at 100 MW ≈ 0.01 ms.

The landscape is fictional. The values on the map show the *type* of effect, not a prediction for a real place.

## Sources

- Hannah Ritchie (2026): [How much electricity does AI consume? (2025 summary)](https://hannahritchie.substack.com/p/ai-electricity-2025)
- IEA (2026): [Key Questions on Energy and AI](https://www.iea.org/reports/key-questions-on-energy-and-ai)
- IEA: [Data centres and energy, from global headlines to local headaches](https://www.iea.org/commentaries/data-centres-and-energy-from-global-headlines-to-local-headaches)
- The Register (2026), citing UC Riverside: [AI datacenters may gulp NYC's daily water supply at peak](https://theregister.com/on-prem/2026/03/10/ai-datacenters-may-gulp-nycs-daily-water-supply-at-peak/5228973)
- Berkeley Lab (2024): [United States Data Center Energy Usage Report](https://eta-publications.lbl.gov/publications/2024-lbnl-data-center-energy-usage-report)

## Next steps

- Back the model assumptions (bills, noise, air, water level) with sources
- Projection on a table, calibration, physical cubes with tracking
- Optional: a "your place" mode on OpenStreetMap data
