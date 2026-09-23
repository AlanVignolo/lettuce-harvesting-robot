# Vision modules

Standalone computer-vision scripts, one folder per detector. Each folder can run independently (capture + detect + visualize) for calibration and testing, and is also imported by the supervisor level during normal operation.

Classical CV throughout — no trained models. Each detector was built around whichever color channel actually separates its target from the hydroponic-wall background; see the [main README](../README.md#vision-three-detectors-three-color-channels) for why.

## Folders

- **`Escaner Horizontal/`** — reference tape detection along the horizontal axis (X correction). HSV **V-channel** threshold + contour scoring. See also [`Correccion Posicion Horizontal/`](Correccion%20Posicion%20Horizontal/), which applies the same detector for closed-loop correction during horizontal moves.
- **`Escaner Vertical/`** — tube detection along the vertical axis (row mapping) and tape detection for Y correction. Canny edges + HSV **S-channel** filtering; see its own [README](Escaner%20Vertical/README.md) for usage. [`Correccion Posicion Vertical/`](Correccion%20Posicion%20Vertical/) applies it for closed-loop vertical correction, and [`Escaner Vertical Plantin/`](Escaner%20Vertical%20Plantin/) is a variant tuned for seedlings.
- **`Analizar Cultivo/`** — crop classifier: HSV green segmentation + morphology + contour-area thresholding to classify each station as mature lettuce / immature / empty. See its own [`README_CONFIGURACION.md`](Analizar%20Cultivo/README_CONFIGURACION.md).

## Dependencies

Same as the supervisor level: `opencv-python`, `numpy`, `matplotlib`, `scipy` (see [`Nivel_Supervisor/requirements.txt`](../Nivel_Supervisor/requirements.txt)). Scripts that import `core.camera_manager` or `config.robot_config` expect to be run with `Nivel_Supervisor/` on the Python path (as the supervisor does); the ones without that import can run standalone.
