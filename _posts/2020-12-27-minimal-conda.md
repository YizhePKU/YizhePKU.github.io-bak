# A minimal guide to Conda

**Hint:** If you forget commands often(like me), go install [tldr](https://github.com/tldr-pages/tldr). Try it, it's awesome.

## When to use Conda/Virtualenv

Both Conda and Virtualenv create seperate Python environments. Virtualenv is lightweight and easier to get started with. On the other hand, Conda has more features. For example, Conda lets you use different Python versions in different environments. Conda also employs an SAT solver for dependency solving.

## Install Conda

When choosing an installer, prefer the smaller [MiniConda][1] over Anaconda. MiniConda comes with no default packages, so you can start with a clean slate.

Download and run the install script. Restart your shell after installation completes.

By default, Conda will activate `base` environment in every shell you create. If you don't like it, run `conda config --set auto_activate_base false`.


## Using Conda

Conda's command line interface is somewhat unintuitive and inconsistent. Here're the most useful commands to get you started(use `tldr` in case you forget some of them):

* `conda env list` to list all environemnts.
* `conda create --name my_env` to create an empty environment.
* `conda activate my_env` to enter an environment.
* `conda install some_package` to add packages to current environment. Note that you can add multiple packages at once, which is usually faster.
* `conda deactivate` to exit the current environment.

These commands are great for trying things out. However, once you've decided which packages to use, you should pin it down for reproductivity. Conda uses YAML as its environment file format. Here is an example environment file:

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

Save it to a file, say `requirement.txt`, you can then run `conda env create -f my_env.yml` to recreate the environment.

Do not confuse `conda env create` with `conda create`; the former creates environments from file, while the latter creates environment interactively.

[1]: https://docs.conda.io/en/latest/miniconda.html
