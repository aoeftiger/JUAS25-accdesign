[![DOI](https://zenodo.org/badge/752701535.svg)](https://zenodo.org/doi/10.5281/zenodo.10877902)

# Joint Universities Accelerator School 2025: Accelerator Design Workshop

The [JUAS](https://www.esi-archamps.eu/juas-presentation/) 2025 features an accelerator design workshop. This repository provides the lattice design jupyter notebook, which contains the setup and exercises to design a particle collider.

This repository provides a `cpymad` and `MAD-X` configuration for running jupyter notebooks, locally inside a docker container or on [mybinder.org](https://mybinder.org/).

Launch an interactive binder instance here:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/aoeftiger/JUAS25-accdesign/v1.2)

The published docker image is found here:

[![Docker](https://shields.io/docker/image-size/aoeftiger/juas24-accdesign?logo=docker)](https://hub.docker.com/r/aoeftiger/juas25-accdesign)

## Running the container
The docker container can be run on the command line via

    JUPYTER_TOKEN=madx docker run -p 8880:8888 -e JUPYTER_TOKEN -e CHOWN_HOME=yes -e CHOWN_HOME_OPTS='-R' -v $HOME:/home/jovyan/home/ aoeftiger/juas25-accdesign

where

 - `JUPYTER_TOKEN=madx` sets the token (password) for entering the jupyter server
 - `-p 8880:8888` forwards the jupyter server port from inside the container to your outside system (change the first port `8880` to your liking)
 - `-v $HOME:/home/jovyan/home` binds your home directory to inside the docker container such that you can save and load notebooks.

Next you can open your browser and load the page [https://localhost:8880/?token=madx](https://localhost:8880/?token=madx) to connect to the running jupyter lab server.

## Building locally
The docker container for this repository can be built locally by running on the command line

    docker build -t aoeftiger/juas25-accdesign .

## Troubleshooting
If you face permission issues with accessing your home directory from within the container, you might want to provide your user ID and group ID explicitly to the container as a solution.

On linux, check your user and group IDs via the CLI command `$ id` and use these values when running the container as above but with the additional arguments:

    [...] --user root -e NB_UID=<your user id> -e NB_GID=<your group id> [...]

Add these comments before the mount instruction `-v [...]`.

For further information, follow [the guide on jupyter-docker-stacks.readthedocs.io](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/troubleshooting.html#permission-denied-when-mounting-volumes), see specifically the second point under "Some things to try".

