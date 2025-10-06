# RamaLama Container for Llama.cpp Source

The llamacpp-src repository is provided for reproducibility purposes. It packages the source code used in each run of the llama.cpp runtime. 

## What are RamaLama Containers?

RamaLama produces three broad types of OCI compatible artifacts:

1. Raw AI models (e.g. gguf, safetensors)
2. Hardware optimized runtimes (e.g. llama.cpp, vLLM)
3. Prebuilt model images which combine a model and runtime together.
   
By default our runtime builds come packaged with an [openai API](https://platform.openai.com/docs/api-reference/introduction) compatible web server you can use to immediately interact with your deployed agent. However, our runtime builds can be used as secure base images to customize deployments for your needs.


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