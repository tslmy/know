---
description: Works for me. Twice.
---

# How to Install auto-sklearn on macOS 10.14~10.15

## via Docker

Easiest way of using auto-sklearn on macOS is via Docker. Make sure your Docker is running, and execute:

```bash
docker run -it -v $PWD:/opt/nb -p 8888:8888 felixleung/auto-sklearn /bin/bash -c "pip install --upgrade pip auto-sklearn tables tqdm && cd /opt/nb && ipython"
```

Here, `pip install --upgrade pip ...` upgrades the `auto-sklearn` module \(along with its dependencies\) and installs a couple of others that I found useful. This command gives you an iPython REPL with current working directory as, well, current working directory.

This is, however, not the most ideal solution if you already have a Python envrionment / pipeline / JupyterLab setup that you would like to stick with. In that case, you will need to **build from scratch**.

## Build from Scratch

Make sure you have Homebrew installed.

```bash
xcode-select --install # install command line tools
export MACOSX_DEPLOYMENT_TARGET=10.14
brew install swig
brew install gcc@8
export CC=gcc-8
# Build XGBoost (from <https://xgboost.readthedocs.io/en/latest/build.html#building-on-osx>):
git clone --recursive https://github.com/dmlc/xgboost
cd xgboost # The original tutorial didn't have this
mkdir build
cd build
CXX=g++-8 cmake .. # I changed 8 to 9 and it also worked
make -j4
# Move the compiled binary library to the directory where python-xgboost will look for it -- there's probably better ways to achieve this:
mkdir ~/miniconda3/xgboost # Notice that I use `miniconda3` for managing packages.
cp ../lib/libxgboost.dylib ~/miniconda3/xgboost
# Clean up XGBoost installation:
cd ../../
rm -rf xgboost
# Install other auto-sklearn dependencies:
curl https://raw.githubusercontent.com/automl/auto-sklearn/master/requirements.txt | xargs -n 1 -L 1 pip install
# Install auto-sklearn:
pip install auto-sklearn --user
```

Not sure why, but `pandas` and/or `numpy` may fail to load after installing `auto-sklearn`. This can be fixed by upgrading these two modules:

```bash
pip install --upgrade pandas numpy
```

