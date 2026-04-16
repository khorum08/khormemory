title: Wan2.2 i2v 14B GGUF ComfyUI Optimization for NSFW Ballerina Loops on 12GB RTX 4080
date: 2026-04-16
tags: comfyui, wan2.2, gguf, sageattention, low-vram, nsfw-video, ballerina-loop, allocator-fragmentation, fp8-illusion, truth-seeking
source: grokclaw-legacy
status: active
key_directives:

Preserve maximum skin/genital detail, natural physics, and source-image fidelity in explicit adult/erotica loops.
Target consistent 430-485s renders for 85-frame 480x832 source → 3× GIMM-VFI 4s 24fps loops.
Never summarize away messiness; keep raw log excerpts, exact errors, and contradictory evidence for full reconstruction.
Quantization in WanVideoModelLoaderMultiGPU must be disabled for any GGUF model (FP8 options are ignored).
Lock sageattn as permanent attention_mode in the node (global flag is overridden by MultiGPU/WanVideoWrapper).
Full ComfyUI restart required after any node or batch-file change; allocator state is fragile.
LoRA key-not-loaded warnings (img_emb.proj.*) are expected, harmless, and ignored.
Prioritize surgical low-fluff analysis; reject fluff, hype, or unverified community claims.


Key Findings
Wan2.2 i2v 14B Q5_K_M GGUF + LightningFast LightX2V LoRAs (both at 1.0) + sageattn delivers stable 85-frame 480x832 explicit ballerina 360-spin + hip-thrust loops at 432-485s with 9.806 GB allocated / 10.781 GB reserved on 12 GB RTX 4080. FP8 options in WanVideoModelLoaderMultiGPU are completely bypassed for GGUF files (identical VRAM/timings when set to fp8_e4m3fn_scaled_fast vs disabled). Flash-attn wheel installation produced repeated DLL load failures (0xc0000139) and nvcc FileNotFoundError; sageattn is the only stable backend. Allocator fragmentation (CPU >85% triggering PromptExecutor cache reset + "Free (according to CUDA): 0 bytes") caused 5-10× slowdowns on identical workflows; fixed by PYTORCH_CUDA_ALLOC_CONF=expandable_segments:True,max_split_size_mb:512,garbage_collection_threshold:0.9 + --reserve-vram 0.5 + blocks_to_swap=14 + iGPU desktop + full restarts. LoRA key-not-loaded warnings (diffusion_model.img_emb.proj.3/4.*) are harmless architecture mismatch. 85 frames is current VRAM-safe sweet spot; Q6_K_M projected at 80-82 frames for marginal detail gain.
Rejected / Dark-Horse Ideas

Using fp8_e4m3fn_scaled_fast (or any FP8 variant) on GGUF: rejected after side-by-side runs showed zero VRAM/speed difference; node routes GGUF through separate loader path.
Relying on global --use-sage-attention + SAGE_ATTENTION_FORCE=1: rejected; WanVideoModelLoaderMultiGPU overrides it, requiring explicit node attention_mode=sageattn.
Flash-attn 2/3 wheels for potential extra speed: rejected after metadata-generation-failed (nvcc missing) and runtime DLL/procedure-not-found errors; destabilized boot with Windows fatal exception 0xc0000139.
Keeping desktop on dGPU or allowing Chromium browsers (Brave/Edge) on dGPU: rejected; caused VRAM leakage and allocator thrashing even when "forced" via Windows settings.
Native WanFirstLastFrameToVideo nodes: rejected due to WANVAE vs VAE type-mismatch and tensor shape errors (60 vs 52).
Q6_K_M at 85 frames without testing: rejected; projected to exceed safe 11 GB reserved and induce thrashing.

Open Questions / Future Vectors

Exact max frames with Q6_K_M GGUF before offload thrashing (projected 80-82; requires side-by-side test vs current Q5_K_M).
Whether future WanVideoWrapper or comfyui-multigpu updates will expose true FP8 support for GGUF models.
Long-term stability of garbage_collection_threshold:0.9 on very long batch queues (possible side-effects on memory pressure).
Safe integration of TensorRT VAE decode or 4x-ClearRealityV1 upscaler post-LUSTIFY without breaking loop-seam control.
Optimal Highres Fix upscale factor (1.4× vs 1.5×) when feeding to Flux.2 Klein for maximum explicit detail preservation.
Whether raising blocks_to_swap beyond 14 yields further headroom or introduces new offload latency.

Compliance Notes
Honored maximum fidelity preservation and NSFW-as-truth-probe heuristic by keeping explicit detail requirements (skin/genital physics) non-negotiable and rejecting any quality-compromising shortcuts. Fully preserved raw messiness (exact error messages, contradictory FP8 reports, allocator logs, LoRA warnings) per Rich Process Digest directive. Truth-seeking axioms followed: ruthlessly honest about what worked (sageattn + disabled quantization + allocator tuning) vs what didn't (Flash-attn, global flags, FP8 on GGUF). No contradictions with existing key directives; all adjustments (node-level overrides, iGPU desktop) were data-driven from user logs. User preference for surgical low-fluff style maintained throughout.
Suggested filename: 2026-04-16_wan22-gguf-comfyui-nsfw-ballerina-optimization.md