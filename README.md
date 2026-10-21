# PESC.tool.WindingSchem
Winding Layout Calculator

Open [winding_visualizer.html](winding_visualizer.html) in a browser for the standalone winding calculator, with linear and circular views, inner and outer stators, Y/delta connections, and SVG/PNG export. All JavaScript and CSS are embedded; no installation, server, or external dependencies are required.

The interface is organized into Winding Parameters, Winding Properties, View Options, and Winding Animation. Motor inputs and manual schemes are at the top; the compact properties section starts with the winding scheme. Factor details are collapsed by default and show a harmonic spectrum plot with hover values when expanded.

Use **Calculate winding** after editing slots, poles, or a manual scheme. Layers, Y/delta termination, coil shortening, coil connection, and parallel branch changes update the diagram automatically.

The linear view supports distributed slot windings, including layer pairing and coil shortening. Matching labels at the left and right edges identify the same coil crossing the linear diagram boundary.

Use **Coil connection** to choose series, parallel, series/parallel, or series/antiparallel, then choose the number of parallel branches per phase. Unavailable choices are disabled. The default remains all series; Y/delta termination is independent of the coil grouping. Branch labels and the expandable connection table identify each branch's coils and symmetry-group orientation. Both views and image exports use the selected connection plan.

The connection rules use `Ns` = slots, `p` = total poles, and `nlay` = conductor layers:

```text
sym = gcd(Ns, p)                         (two layers)
sym = gcd(gcd(Ns, p), Ns/6)              (one layer)
sphsym = (Ns/3) / sym * (nlay/2)
```

One symmetry group permits series only. One coil per symmetry group permits any connection. Otherwise, odd `p/2` requires series/antiparallel and even `p/2` permits series/parallel. Branch counts must divide `sym`; each branch contains complete symmetry groups with equal coil counts. The calculator also checks equivalent coil positions, spans, group polarity, and matching oriented fundamental EMFs before offering a parallel arrangement. Patterns outside these rules retain series only. Antiparallel reverses opposite groups' reference terminals; the displayed coil arrows already include this correction.

Examples: 12 slots / 10 poles / two layers offers two series/antiparallel branches; 18 / 16 offers two series/parallel branches; 12 / 8 offers four individual coils in parallel or two branches with two coils each.
