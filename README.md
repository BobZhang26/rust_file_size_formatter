# Rust project template

In this template, I used Visual Studio Code to create a new Codespace configuration with dev containers.

```json
// For format details, see https://aka.ms/devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/rust
{
	"name": "Rust",
	// Or use a Dockerfile or Docker Compose file. More info: https://containers.dev/guide/dockerfile
	// "image": "mcr.microsoft.com/devcontainers/rust:1-1-bullseye",
	"build": {
		"dockerfile": "Dockerfile",
		"context": ".."
	},
	"customizations": {
		"vscode": {
			"extensions": [
				"GitHub.copilot"
			]
		}
	}
}
```

Use the Rust image for the configuration. The image is loaded from a Dockerfile
```python
FROM mcr.microsoft.com/devcontainers/rust:1-1-bullseye
RUN apt-get update 
```
