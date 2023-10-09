# OneClick UI

This is a testbed for running [TheBloke's OneClickUI for docker LLM](https://github.com/TheBlokeAI/dockerLLM) in a local docker environment.

This allows for testing configurations before using a [RunPod](https://runpod.io) template.

## QuickStart

run the following commands in your shell:

1. Create a workspace folder as this will be mounted by the compose project.
```sh
mkdir workspace
```

2. Start the compose project (runs in the background)
```sh
docker compose -p tgw --project-directory . -f ./docker-compose.yml up -d
```

## Customizing

Once this container is up and running, you might want to play around with the `settings.yml` in the `text-generation-webui` project.

An example `settings.yaml` would be saved in the `workspace/text-generation-webui/settings.yaml` folder.  This can be extended from the `workspace/text-generation-webui/settings-template.yaml` A use case for this would be testing the [TextGeneration WebUI Extensions](https://github.com/oobabooga/text-generation-webui/blob/main/docs/Extensions.md).

```yaml
dark_theme: true
show_controls: true
start_with: ''
mode: chat
chat_style: cai-chat
prompt-default: QA
prompt-notebook: QA
preset: simple-1
max_new_tokens: 200
max_new_tokens_min: 1
max_new_tokens_max: 4096
seed: -1
negative_prompt: ''
truncation_length: 2048
truncation_length_min: 0
truncation_length_max: 32768
custom_stopping_strings: ''
auto_max_new_tokens: false
max_tokens_second: 0
ban_eos_token: false
custom_token_bans: ''
add_bos_token: true
skip_special_tokens: true
stream: true
name1: You
character: Assistant
instruction_template: Alpaca
chat-instruct_command: |-
  Continue the chat dialogue below. Write a single reply for the character "<|character|>".

  <|prompt|>
autoload_model: false
default_extensions:
- api
- gallery
- openai
- sd_api_pictures
- send_pictures
- superbooga
- whisper_stt


openai-port: 5001
openai-embedding_device: cuda
openai-sd_webui_url: http://0.0.0.0:7860
openai-debug: 1
sd_api_pictures-manage_VRAM: 1
sd_api_pictures-save_img: 1
sd_api_pictures-prompt_prefix: "(Masterpiece:1.1), detailed, intricate, colorful, (solo:1.1)"
sd_api_pictures-sampler_name: "DPM++ 2M Karras"
```

## Testing

There are some examples from the [TextGeneration WebUI repo](https://github.com/oobabooga/text-generation-webui) in the `examples` folder.  This can be tested in the `web` container interactive or another option would be to set up a local Python virtualenv.  The steps for this are as follows.

The following steps should only be executed once.

1. Create a virtualenv in the project folder.

```sh
python -m venv .venv
```

2. Activate the virtualenv

```sh
source .venv/Scripts/activate
```

3. Load a model (in this case we're using [TheBloke_Mistral-7B-OpenOrca-GPTQ](https://huggingface.co/TheBloke/Mistral-7B-OpenOrca-GPTQ))

using the web interface at http://localhost:7860

4. Install the requirements 

```sh
pip install -r requirements.txt
```

The following steps can be repateated 

1. Run an example

```sh
cd examples/openapi

python openapi-example.py
```

Expected result:

```
❯ python openapi-example.py 
The math problem given in this task has been solved, resulting in the equation being equal to 8 as follows: 2 + 2 equals 4 and then you add another 2 which makes it equal to 6, so when you put two sixes together, we get eight. Therefore, the solution for 4+4 would equate to 8 and the answer to your equation will be 'eight'.
```

## Notes

- Expects CUDA (Nvidia GPU)
- Running examples locally requires Python3