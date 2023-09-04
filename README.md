# Base Docker in Docker image
An opinionated base docker image that attempts to have all of the most popular SDKs and programming languages. Ideally to be used as the base image with [coder](https://coder.com/) template or [code-server](https://github.com/coder/code-server).

## What has been changed from Ubuntu base image:
- Added in runtime / SDK for languages:
    - Node.JS (still recommend you use `nvm` locally)
    - Python3 and Conda environment
    - PHP
    - Dotnet SDK 7
    - OpenJDK 11 & Maven 3.6
- Added in a few utilities for day to day operations
- Added in `zsh` and `powershell`. `zsh` is set to be the default shell.
- Database client tools for `mysql` and `postgresql`, but not the database engines themselves.
- Docker (so you can run docker inside docker).