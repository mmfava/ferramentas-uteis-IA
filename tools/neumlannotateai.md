---
title: neuml/annotateai
owner: neuml
source: https://github.com/neuml/annotateai
description: 📝 Automatically annotate papers using LLMs
stars: 245
tags:
  - nlp
  - artificial-intelligence
  - scientific-papers
  - vector-search
  - large-language-models
  - llm
  - python
created: 2025-01-07
resume: "`annotateai` automatiza a anotação de artigos científicos usando LLMs, fornecendo contexto e resumo para facilitar a leitura."
aliases:
---
## README

[![](https://raw.githubusercontent.com/neuml/annotateai/master/logo.png)](https://raw.githubusercontent.com/neuml/annotateai/master/logo.png)

**Automatically annotate papers using LLMs**

 [![Version](https://camo.githubusercontent.com/fe17059dc9e0c7b95c7b47cf928b48d9e7d81508487e9015ed2c8197c4bef6c0/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f72656c656173652f6e65756d6c2f616e6e6f7461746561692e7376673f7374796c653d666c617426636f6c6f723d73756363657373)](https://github.com/neuml/annotateai/releases)[![GitHub Release Date](https://camo.githubusercontent.com/3be57dd08b8e20117aacfea340af20009bb3783a805224c40a173539b0dab531/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f72656c656173652d646174652f6e65756d6c2f616e6e6f7461746561692e7376673f7374796c653d666c617426636f6c6f723d626c7565) ](https://github.com/neuml/annotateai/releases)[![GitHub issues](https://camo.githubusercontent.com/0ed17f85ee04262d68d2b7e7aad860a85bd66929f1052af37a235390b1815bb8/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6973737565732f6e65756d6c2f616e6e6f7461746561692e7376673f7374796c653d666c617426636f6c6f723d73756363657373) ](https://github.com/neuml/annotateai/issues)[![GitHub last commit](https://camo.githubusercontent.com/4fc03db889b04f5d9bc0621ac8ddc6c1cb2a7de9f6f5ddc93f334ad8559e9ab7/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6173742d636f6d6d69742f6e65756d6c2f616e6e6f7461746561692e7376673f7374796c653d666c617426636f6c6f723d626c7565)](https://github.com/neuml/annotateai)

---

[![demo](https://raw.githubusercontent.com/neuml/annotateai/master/demo.png)](https://raw.githubusercontent.com/neuml/annotateai/master/demo.png)

`annotateai` automatically annotates papers using Large Language Models (LLMs). While LLMs can summarize papers, search papers and build generative text about papers, this project focuses on providing human readers with context as they read.

## Architecture

[![architecture](https://raw.githubusercontent.com/neuml/annotateai/master/images/architecture.png#gh-light-mode-only)](https://raw.githubusercontent.com/neuml/annotateai/master/images/architecture.png#gh-light-mode-only) [![architecture](https://raw.githubusercontent.com/neuml/annotateai/master/images/architecture-dark.png#gh-dark-mode-only)](https://raw.githubusercontent.com/neuml/annotateai/master/images/architecture-dark.png#gh-dark-mode-only)

A one-line call does the following:

- Reads the paper
- Finds the title and important key concepts
- Goes through each page and finds sections that best emphasis the key concepts
- Reads the section and builds a concise short topic
- Annotates the paper and highlights those sections

## Installation

The easiest way to install is via pip and PyPI

```
pip install annotateai
```

Python 3.9+ is supported. Using a Python [virtual environment](https://docs.python.org/3/library/venv.html) is recommended.

`annotateai` can also be installed directly from GitHub to access the latest, unreleased features.

```
pip install git+https://github.com/neuml/annotateai
```

## Examples

`annotateai` can annotate any PDF but it works especially well for medical and scientific papers. The following shows a series of examples using papers from [arXiv](https://arxiv.org/).

This project also works well with papers from [PubMed](https://pubmed.ncbi.nlm.nih.gov/), [bioRxiv](https://www.biorxiv.org/) and [medRxiv](https://www.medrxiv.org/)!

### Setup

Install the following.

```
# Change autoawq[kernels] to "autoawq autoawq-kernels" if a flash-attn error is raised
pip install annotateai autoawq[kernels]

# macOS users should run this instead
pip install annotateai llama-cpp-python
```

The primary input parameter is the path to the LLM. This project is backed by [txtai](https://github.com/neuml/txtai) and it supports any [txtai-supported LLM](https://neuml.github.io/txtai/pipeline/text/llm/).

```
from annotateai import Annotate

# This model works well with medical and scientific literature
annotate = Annotate("NeuML/Llama-3.1_OpenScholar-8B-AWQ")

# macOS users should run this instead
annotate = Annotate(
  "bartowski/Llama-3.1_OpenScholar-8B-GGUF/Llama-3.1_OpenScholar-8B-Q4_K_M.gguf"
)
```

### Annotate paper "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks"

This paper proposed RAG before most of us knew we needed it.

```
annotate("https://arxiv.org/pdf/2005.11401")
```

[![rag](https://raw.githubusercontent.com/neuml/annotateai/master/images/rag.png)](https://raw.githubusercontent.com/neuml/annotateai/master/images/rag.png)

*Source: [https://arxiv.org/pdf/2005.11401](https://arxiv.org/pdf/2005.11401)*

### Annotate paper "HunyuanVideo: A Systematic Framework For Large Video Generative Models"

This paper builds the largest open-source video generation model. It's trending on [Papers With Code](https://paperswithcode.com/) as of Dec 2024.

```
annotate("https://arxiv.org/pdf/2412.03603v2")
```

[![video](https://raw.githubusercontent.com/neuml/annotateai/master/images/video.png)](https://raw.githubusercontent.com/neuml/annotateai/master/images/video.png)

*Source: [https://arxiv.org/pdf/2412.03603v2](https://arxiv.org/pdf/2412.03603v2)*

### Annotate paper "OpenDebateEvidence: A Massive-Scale Argument Mining and Summarization Dataset"

This paper was presented at the `38th Conference on Neural Information Processing Systems (NeurIPS 2024) Track on Datasets and Benchmarks`.

```
annotate("https://arxiv.org/pdf/2406.14657")
```

[![debate](https://raw.githubusercontent.com/neuml/annotateai/master/images/debate.png)](https://raw.githubusercontent.com/neuml/annotateai/master/images/debate.png)

*Source: [https://arxiv.org/pdf/2406.14657](https://arxiv.org/pdf/2406.14657)*

### LLM APIs and llama.cpp

As mentioned earlier, this project supports any [txtai-supported LLM](https://neuml.github.io/txtai/pipeline/text/llm/). Some examples below.

```
pip install txtai[pipeline-llm]
```

```
# LLM API services
annotate = Annotate("gpt-4o")
annotate = Annotate("claude-3-5-sonnet-20240620")

# Ollama endpoint
annotate = Annotate("ollama/llama3.1")

# llama.cpp GGUF from Hugging Face Hub
annotate = Annotate(
  "bartowski/Llama-3.1_OpenScholar-8B-GGUF/Llama-3.1_OpenScholar-8B-Q4_K_M.gguf"
)
```

### Additional parameters

The default mode for an `annotate` instance is to automatically generate the key concepts to search for. But these concepts can be provided via the `keywords` parameter.

```
annotate("https://arxiv.org/pdf/2005.11401", keywords=["hallucinations", "llm"])
```

This is useful for situations where we have a large batch of papers and we want it to identify a specific set of concepts to help with a review.

The progress bar can be disabled as follows:

```
annotate("https://arxiv.org/pdf/2005.11401", progress=False)
```

## Docker Web Application

 [![app](https://raw.githubusercontent.com/neuml/annotateai/master/images/app.gif)](https://raw.githubusercontent.com/neuml/annotateai/master/images/app.gif) [![app](https://raw.githubusercontent.com/neuml/annotateai/master/images/app.gif)

](https://raw.githubusercontent.com/neuml/annotateai/master/images/app.gif)[neuml/annotateai](https://hub.docker.com/r/neuml/annotateai) is a web application available on Docker Hub.

This can be run with the default settings as follows.

```
docker run -d --gpus=all -it -p 8501:8501 neuml/annotateai
```

The LLM can also be set via ENV parameters.

```
docker run -d --gpus=all -it -p 8501:8501 -e LLM=bartowski/Llama-3.2-1B-Instruct-GGUF/Llama-3.2-1B-Instruct-Q4_K_M.gguf neuml/annotateai
```

The code for this application can be found in the [app folder](https://github.com/neuml/annotateai/tree/master/app).

## Further Reading

- [Introducing AnnotateAI](https://medium.com/neuml/introducing-annotateai-aecda8851ce5)

