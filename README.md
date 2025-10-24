# MICROMAMBA 🐍

This repository demonstrates usage of micromamba to manage your Python environment :D

## Table of Contents
- [Installation](#installation)
- [Create Environment](#create-environment)
- [Activate Environment](#activate-environment)
- [New Modules for Environment](#new-modules-for-environment)
- [Store Dependencies](#store-dependencies)
- [Update Environment File](#update-environment-file)
- [One-liner](#one-liner)
- [Deactivate Environment](#deactivate-environment)
- [Removing Environment](#removing-environment)

## Installation

Use nix to install micromamba! Trust me it's much easier with nix.  

```bash
# Installing nix
ansible-pull -U https://github.com/brucechanjianle/ansible --ask-become-pass --tags nix
# Installing latest micromamba from nix store (for user)
nix-env -Ai nixpkgs.micromamba
```

Alternatively, you can also use the nix flake file from this project to
install `micromamba`. Sometimes, if you are on older system such as ubuntu22
installation from `nix-env` may fail.  

```bash
# For bash user
nix develop
# For zsh users
nix develop -c $SHELL
```

If you just want a one time thing, you can make a directory and use the
command below:  
```bash
# For bash user
nix develop github:brucechanjianle/micromamba
# For zsh users
nix develop github:brucechanjianle/micromamba -c $SHELL
```

It will drop you into a shell with `micromamba`.  

## Create Environment

For example, you would like to create a new virtual environment
for you jupyterlab, you can run the following command:  

```bash
micromamba create -n jupyterlab jupyterlab -c conda-forge
```

You can also create the virtual environment first without installing
anything dependencies.  

```bash
micromamba create -n my_env python=3.10 -c conda-forge
```

Note to use conda-forge if you don't want to worry about licensing issues.  

## Activate Environment

```bash
micromamba activate my_env
```

If you get the below warning:  
```
'micromamba' is running as a subprocess and can't modify the parent shell.
Thus you must initialize your shell before using activate and deactivate.

To initialize the current zsh shell, run:
    $ eval "$(micromamba shell hook --shell zsh)"
and then activate or deactivate with:
    $ micromamba activate
To automatically initialize all future (zsh) shells, run:
    $ micromamba shell init --shell zsh --root-prefix=~/micromamba
If your shell was already initialized, reinitialize your shell with:
    $ micromamba shell reinit --shell zsh
Otherwise, this may be an issue. In the meantime you can run commands. See:
    $ micromamba run --help

Supported shells are {bash, zsh, csh, xonsh, cmd.exe, powershell, fish}.
critical libmamba Shell not initialized
```

 just follow the information to activate your environment.  
```bash
eval "$(micromamba shell hook --shell zsh)"
micromamba activate my_env
````

## New Modules for Environment

Alright, sometimes you might not know all the dependencies that you required.
But don't fret, you can always update the modules that you need as follows:

```bash
micromamba install -n my_env scipy -c conda-forge -y
```

## Store Dependencies

After creating your environment, you may want to store a copy of the dependencies
in order for you to reproduce it on another system.

First you will need to enter the environment:
```bash
micromamba activate my_env
```

Then run the following command to generate an environment.yaml file:
```bash
micromamba env export > environment.yaml
```

## Update Environment File

To update the environment from a YAML file, add or remove libraries in the YAML file
and run the following command to update the environment:
```bash
micromamba update -n my_env --file environment.yaml
```

## One-liner

If you just want to start your jupyter lab without going into your environment,
you can run the following command.  

```bash
micromamba run -n jupyterlab jupyter lab --port 7777
```

Read more about auto starting your jupyterlab quitely behind the scene in this
[article]().

## Deactivate Environment

```bash
micromamba deactivate
```

## Removing Environment

```bash
micromamba env remove -n my_env
```
