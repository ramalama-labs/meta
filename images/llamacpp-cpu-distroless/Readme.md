# RamaLama Container for llama.cpp Distroless

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
docker pull rlcr.io/ramalama/llamacpp-cuda-distroless:latest
```

These images are usually used as either a secure base image as part of a larger docker build process or can be used to directly serve a model by mounting a model file into the `/models` directory of the running container.

```bash
docker run \
    -p 8080:8080 \
    -v /path/to/your/model.gguf:/models/model.gguf \
    rlcr.io/ramalama/llamacpp-cpu-distroless:latest \
    /usr/local/bin/llama-server -m /models/model.gguf --host 0.0.0.0 --port 8080 --no-warmup
```

### RamaLama CLI

If you're using the [RamaLama CLI](https://github.com/containers/ramalama) you can chat with agents on the commandline 


```bash
ramalama chat
```




## Understanding Image Tags

For a given repository RamaLama produces a variety of convenience tagged images depending on your deployment modality.
These artifacts can either be directly mounted as system volumes if you only need the underlying model artifact or utilized as a complete runnable package when combined with a runtime and/or accelerator.

| **Runtime Type** | **Description** | **Tag Format** | **Examples** | **Notes** |
| -----------------| --------------- | -------------- | ------------ | --------- |
| **Runtime Image**      | Containerized runtime environment built from a specific commit of the source code (e.g., `llama.cpp`, `vLLM`, `text-generation-inference`). | `:<commit>` | `:1eeb523c3e0c7ffbd59469f5463dcbdecba3535e` | Each image is compiled from the tagged codebase commit. Used for reproducibility and binary verification.  |
| **Latest Runtime Tag** | Rolling pointer to the most recent stable or released build of the default runtime.  | `:latest`  | `:latest → :1eeb523c3e0c7ffbd59469f5463dcbdecba3535e`   | Always points to the most recent release of the repository variant. Updated automatically on release publication. |



## Need additional images?

If you need additional architecture targets, alternative runtimes, custom accelerators, or any other combination please contact us [here](https://www.ramalama.com/contact).