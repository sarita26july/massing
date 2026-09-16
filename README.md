Massing
A cinematic, real-time city builder and simulator on real open city data. Fly through a gorgeously lit 3D slice of a real neighborhood, reshape it with the feel of a professional 3D editor, and watch the city respond.

The bar: make a graphics or simulation engineer lean in and ask "this runs in a browser?".

Status
Ground-up rebuild in progress. The repo began as a shadow-honesty decision tool and is being rebuilt into the cinematic simulator described here. The target architecture and the decision log are in docs/architecture.md and docs/decisions.md. The rebuild proceeds in numbered units; the renderer spine (a WebGPU canvas with an automatic WebGL2 fallback) is standing, and the city loader is multi-city.

What it is
A real slice of a real city, every building extruded from its own recorded height, in true local metres. Toronto was first; the loader, the renderer, and the simulation are city-agnostic, and the architecture is pointed at open onboarding of any bounding box.
A WebGPU rendering pipeline: physically based materials, image-based lighting, cascaded sun shadows, and a node-based post stack (GTAO, bloom, fog, AgX tone mapping), tuned for a cinematic look in real time.
A live simulation: time of day driven by real solar position in the city's own time zone, traffic flow on the real street network, and growth, all reacting when you reshape the city.
A professional editor feel: orbit and fly cameras, in-world selection, transform gizmos, and natural-language edits that resolve to the same bounded operations.
Cities
Each city is one folder under data/cities/<id>/ with canonical filenames, resolved through src/model/cities.ts. The app loads Toronto by default and takes ?city=<id>.

id	Neighborhood	Polygons	Heights	Zone
toronto	St. Lawrence, Toronto	1315	City of Toronto 3D Massing 2025, measured	America/Toronto
nyc	Lower Manhattan, New York	1013	NYC Open Data footprints, LiDAR height_roof	America/New_York
nyc-levels	Lower Manhattan (levels variant)	1013	same geometry, heights as the estimated tier	America/New_York
mexico	Cuauhtemoc, Mexico City	172	OSM tags, the thin-data case	America/Mexico_City
A building's height comes from the best available source, in order of trust: city LiDAR, then the OSM height tag, then building:levels times an assumed storey height. The tier rides with the building as HEIGHT_SRC, so a consequence computed from estimated heights reads as less trustworthy than one computed from measured heights. A building with no height in any tier is excluded, never defaulted.

nyc-levels is not a separate neighborhood. It is nyc geometry with the heights relabeled to the weakest tier, the A/B that shows what the confidence model does when the data gets thin.

Onboarding a city is offline and one command, pnpm ingest:city <id>, followed by pnpm verify:structure <id>. The structural gate is not a correctness gate: a city can pass every structural check and still carry garbage heights, which is exactly why the height tier travels with every consequence.

The one line
Spectacle and feel are primary; accuracy is secondary. The one line never crossed is dressing invented simulation as measured authority. Grounded values (real building heights, real road geometry) read as real; simulated values (flow, growth, weather, agents) read as part of the simulated world.
