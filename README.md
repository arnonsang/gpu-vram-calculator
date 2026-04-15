# GPU VRAM Calculator

**GPU Memory Forensics & Infrastructure Calculator for Large Language Models.**

Single-file html designed for engineers, system architects, and local LLM enthusiasts. It provides preliminary memory requirements for the llm models and maps them against a list of hardware.

## Mathematical Methodology

The calculator uses standard industry heuristics to determine the "Memory Wall":

### 1. Weight Memory

$$Memory_{weights} = \frac{Parameters \times BitsPerWeight}{8}$$

### 2. KV Cache Memory (GQA-Aware)

$$Memory_{KV} = \frac{2 \times Layers \times KV\_Heads \times Head\_Dim \times Context \times BytesPerElement}{1024^3}$$

*Where* $Head\_Dim = \frac{HiddenSize}{Query\_Heads}$

### 3. System Floor

Includes a static **2.2 GB floor** to account for CUDA driver stacks, basic activation buffers, and modern kernel overhead (Build 2026.4).

*Disclaimer: These calculations are theoretical minimums. Real-world usage may vary slightly depending on your inference framework (vLLM, llama.cpp, TensorRT-LLM) and runtime activation spikes.*
