# Bonsai Fishtank — Cinematic (Babylon.js)

Head-coupled-perspective bonsai diorama rebuilt on **Babylon.js 9** with cinematic post-processing. Sibling to [`bonsai-fishtank`](../bonsai-fishtank) (the three.js original) but upleveled with real volumetric god rays, DoF, chromatic aberration, film grain, SSAO2, and Hosek-Wilkie atmospheric sky.

## Running

Open `index.html` in a modern browser (Chrome, Edge, Safari 16+). Needs a webcam for head tracking.

Keyboard: **H** toggles the UI on/off.

## What's different from the three.js original

| Feature | three.js version | this (Babylon) |
|---|---|---|
| Sky | Hosek-Wilkie via `three.addons/Sky.js` | Babylon `SkyMaterial` (same model, native) |
| God rays | Additive-plane shader fake + cone-gated particles | Real `VolumetricLightScatteringPostProcess` — occlusion-aware |
| Post-processing | `EffectComposer` + `UnrealBloomPass` only | `DefaultRenderingPipeline` — bloom + DoF + chromatic aberration + grain + vignette + tonemap + FXAA |
| Ambient occlusion | none | `SSAO2RenderingPipeline` |
| Screen-space reflections | none | `SSRRenderingPipeline` (for the ceramic dish) |
| Particles | Custom ShaderMaterial instanced quads | Native `ParticleSystem` (petals + dust) |
| Material model | `MeshPhysicalMaterial` (sheen, clearcoat) | `PBRMaterial` (sheen, clearcoat — same PBR stack) |
| Off-axis projection | Manual `camera.projectionMatrix.makePerspective` | `Matrix.PerspectiveOffCenterRHToRef` + `camera.freezeProjectionMatrix` |
| Face tracking | MediaPipe FaceLandmarker | identical |
| Hand / phone tracking | MediaPipe HandLandmarker | identical |
| Calibration flow | 4-corner finger triangulation | identical |

## HUD sliders

Grouped into **Frame** (physical-geometry calibration), **Scene** (diorama placement), **Sun / atmosphere**, and **Cinematic** (live tweaks to the post pipeline).

## Assets

Only `bonsai-meshy.glb` is needed. Copy it from `../bonsai-fishtank/bonsai-meshy.glb` (same Meshy export).
