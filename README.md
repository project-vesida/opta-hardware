# opta-hardware

Part of [Project Vesida](https://github.com/project-vesida). CERN-OHL-S v2.

Hardware design authority for the Optical Transit Array (OpTA) node and platform: parts catalog,
reference configuration, and the interface specifications a node must meet.

## Reference node

A **node** is one camera: lens, sensor, mount. An **array** is one or more nodes at a site with
shared timing and compute.

| Part | Role | Cost |
|---|---|---|
| SVBONY SV705C (Sony IMX585) | Sensor, 1920x1080 ROI at 25 fps | $249 |
| 7Artisans 25 mm f/0.95 | Optics, 23.9 arcsec/px | $239 |
| Mount adapter | | $25 |
| Raspberry Pi 5 | Compute, runs [opta-pipeline](https://github.com/project-vesida/opta-pipeline) | $80 |
| **Per node** | | **$593** |

Four nodes plus the shared platform (GNSS timing, power, enclosure, connectivity) fit under the
$3k array ceiling. The selection is trade study T-01 in
[opta-engineering/SYSTEMS.md](https://github.com/project-vesida/opta-engineering/blob/main/SYSTEMS.md).

| File | Contents |
|---|---|
| [CATALOG.md](CATALOG.md) | Current lens and camera options, mount compatibility, per-node cost |

Machine-readable parts live in opta-model's
[hardware catalog](https://github.com/project-vesida/opta-model/tree/main/src/opta_model/configs/hardware_catalog)
(`cameras.yaml`, `lenses.yaml`, `profiles.yaml`, `sensor_modes.yaml`). Add a part there; describe it here.

## Interfaces this repository owns

- **I-01, sensor frames**: one FITS file per frame with `DATE-OBS`, `NODE-ID`, `EXPTIME`, `INSTRUME`, `GAIN`, `TEMP`. The pipeline's [interfaces doc](https://github.com/project-vesida/opta-pipeline/blob/main/docs/interfaces.md) is the normative list.
- **I-05, timing**: GNSS PPS pulse to the compute GPIO; `DATE-OBS` is stamped from the disciplined clock.

## Build roadmap

The repository will add these deliverables, each tracked as an issue:

1. Capture daemon on the Pi 5 writing I-01 FITS from the SV705C at 25 fps.
2. GNSS PPS timestamping into `DATE-OBS`, with a measured timing error budget.
3. Mount adapter and pointing fixture.
4. Enclosure, power, and connectivity for unattended nightly operation.
5. Reproducible assembly guide, drawings, and acceptance checks.
