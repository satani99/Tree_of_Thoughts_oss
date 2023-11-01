# Tree-of-Thoughts for Open-source LLMs
Official implementation for paper [Tree of Thoughts: Deliberate Problem Solving with Large Language Models](https://arxiv.org/abs/2305.10601) for Open-source models using [LocalAI](https://github.com/mudler/LocalAI) / [pplx-api](https://blog.perplexity.ai/blog/introducing-pplx-api).

## Setup
1. Install `tot` package:
```bash
git clone https://github.com/satani99/tree-of-thought-llm.git
cd tree-of-thought-llm
pip install -r requirements.txt
pip install -e .  # install `tot` package
```
2. Set up OpenAI API key and OpenAI API base and store them in environment variables ``OPENAI_API_KEY`` and ``OPENAI_API_BASE`` respectively(see [here](https://help.openai.com/en/articles/5112595-best-practices-for-api-key-safety)).
- Option 1: Using pplx-api
```
OPENAI_API_KEY="your_pplx-api_key"
OPENAI_API_BASE="https://api.perplexity.ai"
```
- Option 2: Using LocalAI
```
OPENAI_API_KEY="your_openai_api_key"
OPENAI_API_BASE="http://localhost:8080/v1"
```

