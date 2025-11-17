# RamaLama Container for DeepSeek Math 7B Instruct

RamaLama provides a variety of base images for deploying production ready AI applications including raw model objects packaged as OCI artifacts to distroless runtimes optimized for cpu, cuda, vulkan and beyond.


## What are RamaLama Containers?

RamaLama produces three broad types of OCI compatible artifacts:

1. Raw AI models (e.g. gguf, safetensors)
2. Hardware optimized runtimes (e.g. llama.cpp, vLLM)
3. Prebuilt model images which combine a model and runtime together.

By default our runtime builds come packaged with an [openai API](https://platform.openai.com/docs/api-reference/introduction) compatible web server you can use to immediately interact with your deployed agent. However, our runtime builds can be used as secure base images to customize deployments for your needs.


## Getting Started

If you need to get up and running as quickly as possible with a specific model simply select your preferred model image and

```bash
docker pull rlcr.io/ramalama/deepseek-math-7b-instruct:latest
docker run -p 8080:8080 rlcr.io/ramalama/deepseek-math-7b-instruct:latest
```

You now have an AI agent ready to answer queries over port 8080.

### RamaLama CLI

If you're using the [RamaLama CLI](https://github.com/containers/ramalama) you can chat with agents on the commandline


```bash
ramalama chat
```

### Model Artifacts

Model artifacts will be mounted under the `/models` directory.


## Understanding Image Tags

For a given repository RamaLama produces a variety of convenience tagged images depending on your deployment modality.
These artifacts can either be directly mounted as system volumes if you only need the underlying model artifact or utilized as a complete runnable package when combined with a runtime and/or accelerator.

| **Variant**   | **Description**    | **Tag Format**             | **Examples**   | **Notes**   |
| ------------- | ------------------ | -------------------------- | -------------- | ----------- |
| **Model**     | Raw model artifact stored as an OCI artifact (e.g., `.gguf`, `.safetensors`, `.bin`).                                    | `:<artifact-type>`         | `:gguf`, `:safetensors`, `:bin` | Represents the unwrapped model file only, no runtime. Used for storage and provenance tracking. |
| **Container** | Executable runtime image for serving or running a model. Includes binaries and dependencies (e.g., `llama.cpp`, `vLLM`). | `:<runtime>-<accelerator>` | `:llamacpp-cuda`, `:llamacpp-cpu`, `:vllm-cuda`, `:vllm-cpu` | Defines runtime and hardware target. The `latest` tag always points to `:llamacpp-cpu`.         |



## Need additional images?

If you need additional architecture targets, alternative runtimes, custom accelerators, or any other combination please contact us [here](https://www.ramalama.com/contact).
