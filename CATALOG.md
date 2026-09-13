# OpTA Hardware Catalog

The machine-readable source of truth is
[`opta-model/src/opta_model/configs/hardware_catalog/`](https://github.com/project-vesida/opta-model/tree/main/src/opta_model/configs/hardware_catalog).
If this document and the YAML disagree, update both together.

## Catalog policy

- Keep one purchasable packaging row per sensor die.
- Prefer stocked lenses with a clear passive-adapter path to M42/CS astro cameras.
- Use linear RAW camera interfaces; tone-mapped consumer video is outside the array design.
- Keep synthetic gate foils in tests rather than presenting them as purchasable parts.
- Re-run `studies/array_selection_report.py` before changing the reference configuration.

## Mount compatibility

IMX585-class USB astro bodies expose an M42x0.75 or CS thread. A passive adapter is feasible when
the lens flange distance exceeds the camera back focus.

| Lens mount | Flange distance | Compatible with 12.5 mm back focus |
|---|---:|---|
| Canon RF / Leica L | 20.0 mm | Yes |
| MFT | 19.25 mm | Yes |
| Sony E / Canon EF-M | 18.0 mm | Yes |
| Fuji X | 17.7 mm | Yes |
| C-mount | 17.526 mm | Yes |
| Nikon Z | 16.0 mm | Yes |

The IMX585 active-area diagonal is 12.8 mm. Every catalog lens must cover the selected sensor's
active area.

## Cameras

| Die | Packaging | Pitch | Resolution and rate | Interface | Price |
|---|---|---:|---|---|---:|
| IMX585 | SVBONY SV705C | 2.9 µm | 3856×2180 at 21 fps | USB RAW | $249 |
| IMX678 | ZWO ASI678MC | 2.0 µm | 3840×2160 at 47.5 fps | USB RAW | $299 |
| IMX662 | Player One Mars-C II | 2.9 µm | 1936×1100 at 60 fps | USB RAW | $199 |
| IMX477 | Raspberry Pi HQ Camera | 1.55 µm | 4056×3040 at 40 fps | MIPI CSI | $50 |
| IMX296 | Raspberry Pi Global Shutter Camera | 3.45 µm | 1456×1088 at 60 fps | MIPI CSI | $50 |
| IMX174 | ZWO ASI174MM | 5.86 µm | 1936×1216 at 128 fps | USB RAW | $599 |

Radiometric parameters are conservative model inputs, not vendor-performance guarantees. Sources
and assumptions belong beside the corresponding presets in `opta-model`.

## Lenses

| Lens | Format | Mounts | Price | Role |
|---|---|---|---:|---|
| 7Artisans 25 mm f/0.95 | APS-C | E, X, Z, RF, EF-M, L, MFT | $239 | Reference baseline |
| Rokinon/Samyang AF 35 mm f/1.4 | Full frame | E | $350 | Astrometric-margin alternative |
| Viltrox AF 85 mm f/1.4 | Full frame | E, Z, X | $320 | Narrow-field alternative |

## Reference imaging configuration

| Part | Cost |
|---|---:|
| SVBONY SV705C | $249 |
| 7Artisans 25 mm f/0.95 | $239 |
| Passive mount adapter | $25 |
| Raspberry Pi 5 | $80 |
| Per node | $593 |

Four reference nodes plus a $220 shared platform fit within the $3,000 mission ceiling. This is a
model baseline, not procurement authority; prices and availability must be refreshed before build.

## Sources

- [7Artisans 25 mm f/0.95](https://7artisans.store/products/25mm-f0-95)
- [SVBONY SV705C](https://www.svbony.com/sv705c-color-planetary-camera/)
- [ZWO ASI174MM manual](https://i.zwoastro.com/zwo-website/manuals/ASI174_Manual_EN_V1.5.pdf)
