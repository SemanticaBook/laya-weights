# Semantica Laya browser weights

Versioned backup of the prepared Laya multilingual weights used by the Semantica web app. The app falls back to this repository if its primary model source cannot be reached or fails integrity checks.

## Model version

- Semantica artifact: `semantica-laya-multilingual-q8e8-2026-10-26.1` (`VERSION`)
- Upstream checkpoint: [`convaiinnovations/laya`, `multilingual/`](https://huggingface.co/convaiinnovations/laya/tree/main/multilingual)
- Upstream checkpoint revision: `7b928d828b7b0e022f929d9bd2e44165aa270148`
- Model family: Laya multilingual, mmBERT-base encoder, approximately 322M parameters, 100+ languages
- Runtime package: ONNX Runtime Web, `q8e8` (int8 block quantized weights, int8 embeddings)
- Source config: 1024-token input, 256-token decision head
- Manifest model data size: 338,118,656 bytes, split into 14 parts with SHA-256 hashes
- License: Apache-2.0; see [`LICENSE`](LICENSE) and [`NOTICE.md`](NOTICE.md)

These files are a derived ONNX export for in-browser inference, not the original `safetensors` checkpoint. Quantization can cause small output differences from the original model. The artifact is not affiliated with ConvAI Innovations.

## Files and web loading

`manifest.json` describes the ONNX graph, tokenizer, config, and checksummed data parts. The core loads the manifest and all its referenced files from this public repository when the primary model host is unavailable:

```text
https://raw.githubusercontent.com/SemanticaBook/laya-weights/main/
```

Keep all files named by the manifest at the repository root. The browser checks chunk lengths and SHA-256 hashes before initializing its local ONNX Runtime session. Keep the repository public so Pages visitors can download it without credentials.

## Updating the backup

Prepare the browser artifact from the official checkpoint with the `semantica_wasm` model build script, review the generated manifest and license notices, update `VERSION` and this README with the upstream revision, then commit the manifest and every file it references together. Do not add raw checkpoints, tokens, or temporary build directories.
