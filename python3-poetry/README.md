## TLai Docker Container - Python3 + Poetry 

This container was built based on guide @ [TLai - python-project-template + Docker Dev Container]

In order to add package dependencies, use ```poetry add```

In order to update the Dockerfile & Poetry configuration after development use:
```DOCKER_BUILDKIT=1 docker build --target=runtime .```

By using VSCode or PyCharms Dev Container functionality, you can use this Docker container as a full-featured development environment. More @ [Visual Studio Code Dev Containers](https://code.visualstudio.com/docs/devcontainers/containers)