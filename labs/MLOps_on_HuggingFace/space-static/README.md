---
title: MLOps BD 0509 Demo
emoji: 🎬
colorFrom: blue
colorTo: indigo
sdk: static
pinned: false
short_description: In-browser text classification demo (transformers.js)
---

# MLOps_BD_0509 — in-browser demo

Fully static, client-side demo for [`AliMokh/MLOps_BD_0509`](https://huggingface.co/AliMokh/MLOps_BD_0509),
a DistilBERT text-classification model.

There is no server: `index.html` loads the model's quantized ONNX weights
(`onnx/model_quantized.onnx` in the model repo) with
[transformers.js](https://huggingface.co/docs/transformers.js) and runs
inference directly in the visitor's browser via ONNX Runtime Web (WASM).

## Why not Gradio-Lite?

Gradio-Lite runs Python in the browser via Pyodide/WebAssembly, but `torch`
has no WASM build, so `transformers` + `torch` inference can't run there.
Calling the Hugging Face serverless Inference API was the other option, but
it only serves a curated set of warm models and returned
`Model not supported by provider hf-inference` for this repo. Exporting to
ONNX and using transformers.js is the way to get genuine, free, fully
client-side inference for an arbitrary fine-tuned model.

## Known limitation

The model's `config.json` has no `id2label` mapping, so predictions show as
`LABEL_0` / `LABEL_1` rather than human-readable class names. Push an
updated `config.json` with an `id2label` field to the model repo to fix
this.
