# How to install Jupyter Notebooks / JupyterLab

**More:**

- [JupyterLab installation](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html)
- [How to install and execute Jupyter Notebook on Ubuntu 18.04](https://medium.com/@joaolggross/how-to-install-and-execute-jupyter-notebook-on-ubuntu-18-04-d5b37159bd8e)
- [How To Set Up Jupyter Notebook with Python 3 on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-jupyter-notebook-with-python-3-on-ubuntu-18-04)
------------------------
The instructions below have been composed of the sources above.

## Prerequisites

- Check that the current python installations (typically both python2 and python3 are installed):
```
python --version
python3 --version
```
- For more details:
```
ls -l /usr/bin/pyth* | more
```

## 1. Installation on Linux using ```pip```

### 1.1 Ensure that packages are up-to-date

```
sudo apt update && sudo apt upgrade
```

### 1.1 Get the additional Python packages

**1.1.1 Additional packages** (not all of these are needed but it's good to have them)
```
sudo apt install python3-pip python3-dev python3-dev python3-numpy cython python3-pytest
```

**1.1.2 Upgrade `pip3`

```
sudo -H pip3 install --upgrade pip
```
Flags:
 - `-H`: sets the home envirnonment
 - `--upgrade`: upgrades pip and takes care the all dependencies are met (very useful flag in general).

**1.1.3 Install Jupyter Notebook,Jupyter Lab and Voila
```
pip install --upgrade notebook
pip install --upgrade jupyterlab
pip install --upgrade voila
```

### 1.2. Start Jupyter Notebook or/and Jupyter Lab
Check that jupyter is now in your path:

```
which jupyter
```
If not, then reboot, otherwise run 
```
jupyter notebook
```
for Notebook or 
```
jupyter lab
```
for Lab.
 
