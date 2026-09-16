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
