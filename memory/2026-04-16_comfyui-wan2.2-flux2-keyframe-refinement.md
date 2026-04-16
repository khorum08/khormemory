title: ComfyUI Wan2.2 + Flux.2 Pre-VFI Keyframe Refinement Pipeline
date: 2026-04-16
tags: comfyui, wan2.2, flux2, vfi, keyframe-refinement, vram-optimization, adult-erotica, 12gb-setup
source: grokclaw-legacy
status: active
key_directives:

Maximize fidelity preservation and temporal consistency in Wan2.2 I2V + Flux.2 refinement
Prioritize explicit/adult content quality without regression or artifacts
Surgical pruning: retain only high-signal insights, error patterns, and reasoning paths
Favor stable, practical pipelines over unstable full-sequence Flux pre-VFI
12 GB VRAM constraint is non-negotiable; batch_size must remain safe


Key Findings

Wan2.2 I2V remains the primary motion generator; Flux.2 Klein is best used for targeted keyframe refinement (every 8–16 frames) rather than full pre-VFI detailing.
Q5_K_M and Q6_K LowNoise variants deliver immediately observable gains in skin pores, hair detail, anatomy precision, and explicit content fidelity compared to Q4.
GIMM-VFI offers superior quality for skin/fluids but is fragile with batch_size > 2 or ds_factor ≠ 1.0; RIFE VFI is more reliable for final interpolation when keyframes have large quality jumps.
Reference latent hack (two-pass KSampler) and standard keyframe extraction + re-insertion provide better temporal consistency than full-sequence Flux detailer on 12 GB hardware.
Persistent Flux.2 Klein crashes (KeyError 't5xxl', NoneType 'device'/'dtype') trace to Qwen GGUF negative conditioning path; positive-only duplicated conditioning or Mistral encoder is more stable.

Rejected / Dark-Horse Ideas

Full-sequence Flux.2 Klein pre-VFI detailer: repeatedly crashed with dtype/NoneType errors; abandoned after exhaustive workarounds failed.
GMFSS Fortuna as primary VFI: broken auto-downloader and cupy issues; replaced by RIFE/GIMM.
Heavy use of SAGE Attention: offered VRAM savings but introduced quality loss in explicit detail; rejected for final renders.
Single-pass high batch_size (65 frames) with Q6: theoretically possible but practically impossible on 12 GB without severe OOM.

Open Questions / Future Vectors

Can Mistral_3_small_flux2_fp8 restore full CLIPTextEncodeFlux stability for Flux pre-VFI?
Is there a stable Flux.2 + ControlNet Tile pre-VFI path that avoids reference latent hack on 12 GB?
Optimal automated keyframe re-insertion node without manual Batch Merge.
Long-term viability of GIMM-VFI at higher interpolation factors with patches.

Compliance Notes

Honored user preference for disciplined hierarchy, maximum fidelity, and surgical pruning throughout exploration.
Avoided unstable full Flux pre-VFI when it repeatedly failed; shifted to keyframe refinement as the discourse-recommended practical solution.
Preserved explicit/adult content quality as non-negotiable; all recommendations prioritize detail retention without regression.
VRAM constraints on 12 GB hardware respected at every step.

Suggested filename: 2026-04-16_comfyui-wan2.2-flux2-keyframe-refinement.md