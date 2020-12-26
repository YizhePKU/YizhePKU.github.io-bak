# A minimal guide to Conda

I used to be a happy user of `pip` and `virtualenv`, until I came across [a library][1] that is only distributed via Conda and not pip. This post serves as a minimal guide to use libraries like that.

## Install Conda

You want [MiniConda][2], not the full Anaconda. It takes less space, and you can always install packages as needed. Also, Anaconda installs default packages in every environment you create, which might cause conflicts later.

Download the install script, `chmod` to make it executable, and run it. The install script will offer to setup your shell; accept that. Note it's not just about setting up $PATH: Conda needs to integrate itself into the shell, so that it can modify environment as it wish.

After installation, restart your shell. By default, Conda will activate a `base` environment in every shell you create. If you don't like it, run `conda config --set auto_activate_base false`.


## Using Conda

Conda's command line interface is somewhat unintuitive and inconsistent, so brace yourself when reading the documentation. Here're the most useful commands to get you started:

* `conda env list` to list all environemnts.
* `conda create --name my_env` to create an empty environment.
* `conda activate my_env` to enter an environment.
* `conda install some_package` to add packages to current environment. Note that you can add multiple packages at once, which is usually faster.
* `conda deactivate` to exit the current environment.

These commands are great for trying things out. However, once you've decided which packages to use, you should write it down for reproductivity. Conda uses YAML as its environment file format. This is an example environment file from one of my personal project:

```yaml
# Name of your environment
name: my_project

# Extra channels to use when searching for packages. Can be empty.
channels:
  - pytorch

dependencies:
  - cudatoolkit=10.1
  - pytorch
  - faiss-gpu
  - pip

  # Packages that should be installed by pip
  - pip:
    - requests
```

Once you have your dependencies written down in a file(say `my_env.yml`), run `conda env create -f my_env.yml` to recreate the environment. **Do not confuse `conda env create` with `conda create`; the former creates environments from file, while the latter creates environment interactively.**


[1]: https://github.com/facebookresearch/faiss/blob/master/INSTALL.md
[2]: https://docs.conda.io/en/latest/miniconda.html
