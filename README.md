# AI_Joe_ComfyUI_Workflows

A curated collection of ComfyUI workflow JSONs for cutting‑edge image‑to‑video and text‑to‑video generation, including ready‑to‑run pipelines for Wan 2.2 (14B), Wan 2.1, and practical templates for FLUX/Krea and ComfyUI API usage patterns.[1][2][3]

- Repository focus: share minimal, reusable ComfyUI JSON workflows that load cleanly and document required models, inputs, and tunable parameters.[3]
- Targets: high‑quality I2V/T2V with Wan 2.2/2.1 14B; flexible prompt‑driven image generation with FLUX/Krea‑style nodes.[2][1]
- Audience: ComfyUI users who prefer direct JSON imports, reproducible configs, and clear model requirements.[3]

## Contents

- flux1_krea_dev_gguf.json — prompt‑centric image generation scaffold compatible with ComfyUI’s workflow JSON schema, suitable as a base for development and API export workflows.[3]
- video_wan2_2_14B_i2v_lx2v.json — Wan 2.2 14B image‑to‑video pipeline (480p/720p) with prompt/camera controls and start‑frame input.[4][2]
- video_wan2_2_14B_i2v_lx2v_long_video_with_scenario.json — long‑form Wan 2.2 I2V workflow with sequencing blocks and scenario prompts for extended narrative shots.[4][2]
- video_wan2_2_14B_i2v_lx2v_unlimited_long_video.json — streaming/loop‑friendly Wan 2.2 I2V setup intended for very long outputs on capable hardware.[2][4]
- video_wan2_2_14B_t2v_lx2v.json — Wan 2.2 14B text‑to‑video template aligned with Wan 2.x T2V conventions.[1][2]
- video_wan2_2_5B_ti2v.json — compact baseline for lower‑VRAM testing with a smaller model footprint before scaling to 14B pipelines.[1][2]

Each JSON adheres to ComfyUI’s workflow JSON schema, enabling direct drag‑and‑drop import or use via the API format when needed.[3]

## Requirements

- ComfyUI recent build with Manager up to date for node compatibility.[5]
- Model files per workflow: the Wan 2.2 I2V 14B pipelines require the high/low noise diffusion weights, UMT5 XXL text encoder, and Wan VAE in their respective folders.[5][2]
  - diffusion_models: wan2.2_i2v_high_noise_14B_fp8_scaled.safetensors, wan2.2_i2v_low_noise_14B_fp8_scaled.safetensors.[5]
  - text_encoders: umt5_xxl_fp8_e4m3fn_scaled.safetensors.[5]
  - vae: wan_2.1_vae.safetensors.[5]
- Hardware: Wan 2.2 14B I2V is resource‑intensive; official guidance indicates very high VRAM requirements, with single‑GPU reference commands for A14B variants and notes about offloading and dtype conversions.[4][2]
- Optional: API export for programmatic runs or remote execution via services that accept ComfyUI API JSON blobs.[6][7]

## Quick Start

1) Update ComfyUI  
- Open ComfyUI Manager → Update ComfyUI → restart to ensure node compatibility for recent Wan/FLUX workflows.[5]

2) Install model files  
- Place Wan 2.2 I2V 14B high/low noise models in models/diffusion_models, UMT5 XXL text encoder in models/text_encoders, and Wan VAE in models/vae as outlined above.[5]
- For T2V or smaller variants, use corresponding Wan 2.x model weights as documented in Wan repositories.[2][1]

3) Import a workflow  
- Drag a JSON from this repo into ComfyUI to load nodes and connections per the schema; ComfyUI will prompt for any missing models.[3][5]

4) Configure inputs  
- I2V: provide a start image and edit the prompt/camera directives in the text nodes; adjust duration/frames as permitted by the workflow and hardware.[2][5]
- T2V: set the text prompt, resolution profile, and sampling parameters consistent with Wan 2.x recommendations.[1][2]

5) Generate  
- Click Run; for long‑form workflows, ensure sufficient VRAM or enable offloading/memory‑saving options where available.[4][2]

## Using These Workflows via API

- Export API JSON: enable “Dev mode Options” in ComfyUI, load a workflow, then “Save (API format)” to produce the API‑ready JSON blob.[7][6]
- Programmatic execution: pass the API JSON to compatible runners or services, updating inputs (prompts, checkpoints, URLs for images) in JSON before submission.[6][7]
- Inputs as URLs or packaged files: API runners commonly accept HTTP URLs, single input files mapped to input.jpg/input.mp4, or zipped directories referenced by relative paths in the JSON.[7][6]

## Workflow Notes and Tips

- Wan 2.2 I2V prompting: concise scene description plus motion/camera directives yields more stable trajectories; start‑frame strongly conditions scene layout.[2][5]
- Resolution and aspect: Wan 2.x pipelines follow input aspect for I2V and expose 480p/720p options; some official commands reference size as area for generation with aspect preserved.[4][2]
- Performance tuning: large 14B models benefit from offloading, reduced precision, and careful batch/sequence settings; official examples reference flags for dtype conversion and offload to fit into available memory.[4][2]
- Schema hygiene: keep node class types and input keys consistent with ComfyUI’s JSON schema to maintain portability across installs and services.[3]
- Remote or automated runs: generic “any ComfyUI workflow” runners accept API JSON and allow prompt/checkpoint substitution at run time, enabling CI or orchestrated pipelines.[8][6][7]

## Related References

- ComfyUI workflow JSON schema and best practices for saving and importing workflows.[3]
- Wan 2.2 I2V A14B usage and single‑GPU example commands, including VRAM guidance and size/aspect behavior.[2][4]
- Practical setup steps for Wan 2.2 I2V (models, folders, updating ComfyUI, start‑frame upload, prompting) in a step‑by‑step guide.[5]
- Wan 2.1 T2V/I2V family overview and resolution/model variants for 1.3B/14B.[9][1]
- Running ComfyUI workflows programmatically or via third‑party services using API JSON, with input handling patterns.[6][7]

## Roadmap

- Add sidecar README per workflow with parameter explanations and suggested defaults for common GPUs.[4][2]
- Provide API‑format variants alongside visual JSONs for immediate programmatic use.[7][6]
- Expand smaller‑footprint video templates for mid‑range hardware using 1.3B/5B models.[1][2]
- Include example launcher configs for zero‑setup local runners that accept generic ComfyUI workflows.[8]

## License

- Workflow JSONs are configuration files intended for educational and interoperability purposes; model files are not distributed here and must be obtained from their official sources under their respective licenses.[2][4]

## Acknowledgements

- ComfyUI community for the robust node ecosystem and documented JSON schema.[3]
- Wan‑Video/Wan‑AI projects for advancing open video generation in the 2.x series with I2V/T2V 14B models.[1][4][2]
- Guides and tools that demonstrate practical installation, model placement, and step‑by‑step runs for Wan 2.2 I2V.[5]
