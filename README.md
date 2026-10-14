# Gummy Bears

A single-file toy: translucent gummy bears on a white table that you can grab, stretch, squash, throw and pour.

Open `index.html` in a recent browser. The only dependency is three.js, loaded from jsDelivr, so the first load needs a connection.

## Playing

- **Drag** any part of a bear to stretch it. The rest of the bear leans after it and wobbles back when you let go.
- **Pull a head up** to stretch the neck and lift the bear; it drops, squashes and hops.
- **Press a head down** to pancake the bear; let go and it launches back up.
- **Flick** to throw. Bears bounce, squash on landing and shove each other out of the way.
- **Tap the table** to startle nearby bears.
- **Flavour swatches** drop a single bear of that flavour; **Pour more bears** drops a handful into a pile.
- **Wobble** sets the jelly from firm to very soft. Several fingers can grab at once on touch screens.

## How it works

- **Soft bodies.** Each bear has ten mass points (head, ears, snout, body, belly, hands, feet) held together by shape matching with a volume-preserving linear mode. Contacts with the table, the screen edges and other bears are solved as position constraints over four substeps per frame.
- **Implicit surface.** Every part is a signed-distance ellipsoid, and the necks, limbs and ears are tapered strands that thin as they stretch. A smooth union melts them into one surface, which marching cubes re-meshes in each bear's own frame. A per-frame time budget keeps that work in check.
- **Material.** The jelly uses `MeshPhysicalMaterial` with transmission, clearcoat and per-vertex thickness, so colour deepens in thick parts and around the rims. A small shader addition fakes the glow of light scattering inside the candy.
- **Shadows.** Soft blobs are multiplied onto the table in each bear's colour.

ACES tone mapping, a procedural studio environment, and a key light plus a back light complete the look. Resolution and mesh detail step down automatically if frames run long.
