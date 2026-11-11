<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Mafdet-AI/mafdet/main/assets/mafdet-lockup-dark.svg">
  <img src="https://raw.githubusercontent.com/Mafdet-AI/mafdet/main/assets/mafdet-lockup.svg" alt="MAFDET" height="64">
</picture>

### Local LLMs that think while you type.

Open-source research on low-latency inference for local models,<br>
on the hardware people actually own.

</div>

---

Chat interfaces make the model wait for Enter. While you type, the GPU sits idle; when you send, a reasoning model first reads your message, then thinks for hundreds of tokens before the first word of its answer. On a mid-range GPU that thinking is the longest wait of all.

We work on taking that wait away. **[MAFDET](https://github.com/Mafdet-AI/mafdet)** starts reasoning about your message while you are still writing it, keeps that reasoning when you edit the text, and reads the message as it grows, so that on Enter most of the work is already done.

| Wait for the first word of the answer, after Enter | Without | With MAFDET |
|---|---|---|
| Qwen3-4B · RTX 2060, 6 GB · 24 word problems, 24/24 correct both ways | 12.2 s | **3.2 s** |
| Qwen3-14B · RTX 2060, 6 GB (most of it on the CPU) | 108 s | **47 s** |
| Qwen3-4B · MacBook Pro M2 Pro, 16 GB | 18.1 s | **5.6 s** |
| Qwen3-14B · MacBook Pro M2 Pro, 16 GB | 32.7 s | **12.1 s** |
| Open WebUI, thinking off, first word · Qwen3-4B, RTX 2060 | 5.4 s | **0.16 s** |

## Projects

| | |
|---|---|
| **[mafdet](https://github.com/Mafdet-AI/mafdet)** | The app (window and terminal) and the engine on llama.cpp: thinking ahead, reading ahead, a model catalog with estimates for your machine, and `mafdet proxy` for Open WebUI. Windows, macOS (Metal), NVIDIA, AMD Radeon (Vulkan), CPU only. |

```bash
pipx install mafdet
mafdet
```

## How we work

- **Measured, not claimed.** Every number in the README comes with its script and its data in [`research/`](https://github.com/Mafdet-AI/mafdet/tree/main/research), and [`research/LOG.md`](https://github.com/Mafdet-AI/mafdet/blob/main/research/LOG.md) records where the work stands and what is next.
- **Exact where it can be.** Reading ahead must match a from-scratch computation token for token (`mafdet judge` ends with 0 errors). Thinking ahead is not exact, so it is measured on answers that can be checked.
- **Negative results too.** A small model gathering notes for a large one, speculative drafts on a GPU too small for them: tried, measured, and written up as what did not work.
- **Small hardware first.** The reference machine is an RTX 2060 with 6 GB of VRAM.

## Help wanted

- **Benchmarks on AMD Radeon cards**, other generations especially: about half an hour of your machine ([how](https://github.com/Mafdet-AI/mafdet#help-wanted-benchmarks-on-an-amd-radeon)).
- **Linux**: the builds and code paths are in place, not tested yet.
- **`mafdet proxy` with Ollama, vLLM, SGLang and LM Studio**: written on their documented APIs, not yet tried for real ([PROXY.md](https://github.com/Mafdet-AI/mafdet/blob/main/PROXY.md)).

Issues and pull requests are welcome on [mafdet](https://github.com/Mafdet-AI/mafdet/issues). Everything is under [Apache-2.0](https://github.com/Mafdet-AI/mafdet/blob/main/LICENSE).

<sub>Named after Mafdet, the ancient Egyptian feline goddess known as "the runner", who struck snakes and scorpions before they could attack.</sub>
