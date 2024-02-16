# Good developer experience

This is a playground to showcase what is the good developer experience in my mind. In this playground, we will use instill-ai's pipeline recipe and API as an example to construct a good developer experience.

```
// Instill AI's recipe

{
  "version": "v1beta",
  "components": [
    {
      "id": "start",
      "resource_name": "",
      "configuration": {
        "metadata": {
          "input": {
            "type": "array",
            "items": {
              "type": "string"
            },
            "instillFormat": "array:string",
            "title": "input"
          }
        }
      },
      "definition_name": "operator-definitions/start"
    },
    {
      "id": "end",
      "resource_name": "",
      "configuration": {
        "input": {
          "result": "${stability_0.output.images}"
        },
        "metadata": {
          "result": {
            "title": "result"
          }
        }
      },
      "definition_name": "operator-definitions/end"
    },
    {
      "id": "stability_0",
      "resource_name": "users/pochun/connectors/st-dev",
      "configuration": {
        "task": "TASK_TEXT_TO_IMAGE",
        "input": {
          "cfg_scale": 7,
          "clip_guidance_preset": "FAST_BLUE",
          "engine": "stable-diffusion-xl-1024-v1-0",
          "height": 512,
          "prompts": "${start.input}",
          "sampler": "K_DPM_2_ANCESTRAL",
          "samples": 1,
          "steps": 30,
          "width": 512
        }
      },
      "definition_name": "connector-definitions/stability-ai"
    }
  ]
}



```

## Principles

- **Fast feedback loop**: The faster the feedback loop, the more productive the developer is.
- **local development**: The development environment should be as close as possible to the production environment.
- **intelligence**: The tools should be smart enough to help the developer to be more productive.
- **automation**: The tools should automate the repetitive tasks.

### CLI

In this playground, CLI focuses on several features:

- PULL: Pull the latest code from the remote.
- PUSH: Push the code to the remote.
- VIEW: Generate a human-readable view that can better visualize what the code is doing
- DIFF: Show the difference between the local and remote code.
- VALIDATE: Validate the code against the best practices.

### System as code

Borrowing the idea from infrastructure as code, we should maintain the whole system using code within the same repository (We call it protocol here). During the development, we can spin up the services using the code. And we can also deploy the services to the production using the same code.

### Intelligent code editor

With the help of VSCode intelligence, we can properly hint users how to write a good protocol for their services.

### CI/CD

The CI/CD pipeline should be able to validate the protocol and deploy the services to production. The production environment should be able to have different branches. Take Vercel for example, they separate environments into "Production", "Preview" and "Development", each environment can have its environment variables. So I can use different sets of 3rd party services for different environments.

### Good starter

Using `giget` and remote repository to store templates. We can provide a better experience for starting a new project.

The experience will be similar to `create astro@latest` and `create-turbo@latest`. Both of them will ask simple questions to construct the starter project for you.

```
1. What is the name of the project?

- We use -t parameters to indicate which template user want to use
```

### Type safety

Each Instill AI's recipe constructs a pipeline, the pipeline will have input and output and can be called by Instill AI's API. This tool will auto-generate the type definition of this pipeline. So the developer can use the type definition to write the application code.

```
inst --gen-type -r /path/to/recipe -o /path/to/output
```
