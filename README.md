# dev-u22

A developer container based on Ubuntu 22.04 LTS.

Primarily intended for use with the .devcontainer project for working
in vscode workspaces.

See https://github.com/epics-containers/.devcontainer

This developer container works well with python projects based on
python3-pip-skeleton but is also generally useful for setting
up developer environments.

See https://diamondlightsource.github.io/python3-pip-skeleton-cli

# Prerequisites

The host folder in this project provides information on setting up a
workstation to run this devcontainer. See [host](host/README.md)
# Features

## Containers in Containers
Docker and Podman CLI and API are supported inside the container. They all
connect to the user podman instance running on the host.

## Kubernetes CLI tools
Inlcudes kubectl, helm and oidc-login. Set environment ``KUBECONFIG`` to
point to your kubectl configuration file in order for these tools to
pick up cluster configuration.

DLS users need to either:

- run ``module load pollux`` before launching the devcontainer.
- add this to $HOME/.bashrc_dev
  - export KUBECONFIG=$HOME/.kube/config_pollux

DLS kubectl users will also need to mount these folders into the container.

- /dls_sw/apps/kubernetes/pollux/
- /dls_sw/apps/kubernetes/argus/

In the .devcontainer project these are commented out in the file
https://github.com/epics-containers/.devcontainer/blob/main/devcontainer.json

Uses the home directory .kube user folder for cluster configuration.

## Global VirtualEnv
This is a feature of .devcontainer project see
https://github.com/epics-containers/.devcontainer/blob/main/Dockerfile

- The virtualenv /venv is already in the path and pre-populated with the
  skeleton dev dependencies.
- You are free to create additional venvs inside the container if the projects
  inside have conflicting dependencies, but this should not usually be needed.

## .bashrc_dev
- This file is mounted as /root/.bashrc and provides a starting point for
  your bash profile inside the container. Includes:
  - autocompletion for git and bash
  - shared bash history with the host
  - will also execute a personal run commands file if found at
    - $HOME/.bashrc_dev

# How to adopt
The best approach to adoption is using vscode devcontainers.

This repo gives details of how to do this:

https://github.com/epics-containers/.devcontainer


# Tips and Tricks

## open in default browser

When reviewing your documentation build you will need to open an html file
in a browser. Rather than installing a browser inside the devcontainer you
can use the [provided vscode plugin](https://marketplace.visualstudio.com/items?itemName=peakchen90.open-html-in-browser).

Simply right-click on the html file in the explorer and choose
"Open in default browser"
