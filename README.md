Massing
A cinematic, real-time city builder and simulator on real open city data. Fly through a gorgeously lit 3D slice of a real neighborhood, reshape it with the feel of a professional 3D editor, and watch the city respond.

The bar: make a graphics or simulation engineer lean in and ask "this runs in a browser?".

Status
Ground-up rebuild in progress. The repo began as a shadow-honesty decision tool and is being rebuilt into the cinematic simulator described here. The target architecture and the decision log are in docs/architecture.md and docs/decisions.md. The rebuild proceeds in numbered units; the renderer spine (a WebGPU canvas with an automatic WebGL2 fallback) is standing, and the city loader is multi-city.
