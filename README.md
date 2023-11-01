# Tree-of-Thoughts for Open-Source LLMs
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
3. If you're using pplx-api then skip this step:
- To setup the LocalAI, clone this [repo](https://github.com/satani99/LocalAI/tree/master) which is for zephyr-7b model, and then download the model to the models directory. If you want to use different model then refer this [guide](https://localai.io/howtos/easy-model-import-downloaded/).
Run the below code in the main directory.
```bash
git clone https://github.com/satani99/LocalAI.git
cd LocalAI
wget https://huggingface.co/TheBloke/zephyr-7B-beta-GGUF/resolve/main/zephyr-7b-beta.Q5_K_M.gguf -O models/zephyr
sudo docker compose up -d --pull always
```

## Experiments
Run experiments via ``sh scripts/game24/{standard_sampling, cot_sampling, bfs}.sh``. It'll run the llama-2-70b-chat model on pplx-api. If you want to run a different model then add the ``--backend`` in any of the above sh files.

e.g. ``--backend zephyr`` choices for the backend(``llama2-7b``, ``llama-2-13b-chat``, ``zephyr``, ``llama-2-70b-chat``, ``mistral-7b-instruct``)

CoT and standard sampling were run for 1000 steps and bfs(ToT) was run for 100 steps.


## Result
The CoT achieved a 1% score(10 out of 1000 steps) and standard IO prompting did better than CoT with a 4.9% success score. However bfs(ToT) didn't give even one true answer, the reasons are discussed below.

## Limitations
- Right now pplx-api doesn't support multiple outputs for one input. So we are restrained to use ``n_generate_sample=1`` and can't get 100 or 10 outputs per input. So we can only evaluate CoT and standard prompting method and using ``n_generate_sample=1`` isn't quite a Tree of Thoughts prompting. So that's why the score is 0.

- In LocalAI, we can get multiple outputs for one input but all the outputs are the same for that input. So it is also same as getting only one output.

## Acknowledgments
Original repos:
[ToT](https://github.com/princeton-nlp/tree-of-thought-llm)
[LocalAI](https://github.com/mudler/LocalAI)
