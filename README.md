# Base Docker in Docker image
An opinionated base docker image that attempts to have all of the most popular SDKs and programming languages. Ideally to be used as the base image with [coder](https://coder.com/) template or [code-server](https://github.com/coder/code-server).

## What has been changed from Ubuntu base image:
- Docker (so you can run docker inside docker).
- Runtimes/SDKs:
    - Node.JS (still recommend you use `nvm` locally)
    - Python3 and Conda environment
    - PHP
    - Dotnet SDK 8
    - OpenJDK 11 & Maven 3.9
    - Golang
    - Rust
- Cloud CLIs:
  - AWS CLI
  - Azure CLI
  - Google Cloud CLI
- Shells:
  - `zsh` (also set to the default user's shell)
  - `powershell`
- Database client tools (but not the DB engines themselves)
  - `mysql-client`
  - `postgresql-client`
- Added in a few utilities for day to day operations
  - `aria2`
  - `cloc`
  - `jq`
  - `imagemagick`
  - `ncdu`
  - `nmap`
  - `mc`
  - `rclone`
  - `ssh` (via `openssh-client`)
  - `terraform`
  - `tmux`
  - `vim`
  - `wget`
