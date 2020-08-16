# For fast installation of software on Ubuntu 20.04 LTS

This may be useful if you just installed Ubuntu 20.04 LTS, no guarantees that this works on any other version. The software collection is based on our own needs (=includes compilers, data analysis, molecular simualtion related stuff, etc.). This has been tried and tested, but mileage may vary.

**A few notes:**

1. There are some redundancies (but that's ok, there's no harm in that)
2. If you follow this using a computer that already has some of the software, check first if it is installed or/and needs to be updated (this concerns mostly the packages installed from git & VMD)
3. The packages from git are installed in `/opt/git`. If you want to do the same, create the directory and change its access rights (or choose another location) and create also directory `git` under `/opt`:
   ```
   cd /opt
   sudo chown ${USER}:${USER} .  
   mkdir git
   ```

## Restricted repository & Ubuntu partner repositories:
This is usually done automatically, but there are variations.
```
sudo add-apt-repository restricted
sudo apt update && sudo apt upgrade
```

- Enable also Ubuntu partner repositories manually from *Software and Updates*

## Install Flatpak
``` 
sudo apt install flatpak gnome-software-plugin-flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
and reboot.

## Packages that need interaction because of licenses or some other reasons:
```
sudo apt install ubuntu-restricted-extras ttf-mscorefonts-installer fonts-mathematica
```
for gnome based systems one may also want install these extras (not required; don't install with KDE):
```
sudo apt install gnome-tweak-tool gnome-shell-extensions
```

## These don't need user interaction (but no guarantees):

But this will take a while (10-40 mins) for the first installation.

There are redundancies (but that doesn't make any difference). These packages take care of the dependencies of the software below, it is easier and faster to just install everything in one go.

```
sudo apt install openssh-server rar unrar p7zip-full p7zip-rar openjdk-11-jdk synaptic git g++ cmake gfortran gnuplot \
gsl-bin grace povray povray-includes povray-doc pdf2svg cairosvg pngtools tkpng epstool ipython3 cython3 automake \
autoconf h5utils openbabel openbabel-gui gawk fonts-mathjax autotools-dev chemical-mime-data fig2dev screen a2ps dvi2ps \
python-opengl ipython3  libpng-tools tachyon doxygen equalx bibutils zlibc mathgl tcl-dev tk-dev tcl-tclreadline \
libfftw3-dev sphinx-common cmake-curses-gui gcc-opt hwloc cpuinfo libhwloc-common libhwloc-dev libconfig++-dev \
freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev build-essential \
gcc-7 g++-7 gcc-8 g++-8 typecatcher fonts-liberation fonts-liberation2 texlive-full emacs emacs-goodies-el ispell \
iamerican-insane ibritish-insane auctex tigervnc-viewer tigervnc-xorg-extension tigervnc-standalone-server xfce4 \
remmina  python3-pip python3-dev python3-dev python3-numpy cython python3-pytest libcairo2-dev \
python3-venv python3-wheel python3-dev libgirepository1.0-dev libbz2-dev libreadline-dev \
libssl-dev zlib1g-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libcairo2-dev \
libgirepository1.0-dev pkg-config gir1.2-gtk-3.0 qt5-default gitk libboost-all-dev libglfw3 libglfw3-dev \\
python3-gpg npm

```
## Have NVIDIA card? Install CUDA 11.0 and NVIDIA Drivers
If not, then skip this.

- **Tested with:** GTX1070M, GTX980M, RTX2070  

**NOTE:** This is for CUDA 11.0 only (files, checksums etc.)
```
cd ~/Downloads
mkdir CUDA
cd CUDA
wget http://developer.download.nvidia.com/compute/cuda/11.0.2/local_installers/cuda-repo-ubuntu2004-11-0-local_11.0.2-450.51.05-1_amd64.deb
md5sum cuda-repo-ubuntu2004-11-0-local_11.0.2-450.51.05-1_amd64.deb
```
Cheksum must match to: 74b09b0a04adad8c283862a1641eaf6c
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo dpkg -i cuda-repo-ubuntu2004-11-0-local_11.0.2-450.51.05-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu2004-11-0-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
```
```
export PATH=/usr/local/cuda-11.0/bin${PATH:+:${PATH}}
```
you must put this also in your `.profile`.

**REBOOT.**

```
The following may give troubke but it is not critical:

/usr/bin/nvidia-persistenced --verbose
```
```
cat /proc/driver/nvidia/version
```
These tests should pass:
```
cuda-install-samples-11.0.sh ~/Downloads/CUDA
cd ~/Downloads/CUDA/NVIDIA_CUDA-11.0_Samples
make 
./bin/x86_64/linux/release/deviceQuery
./bin/x86_64/linux/release/bandwidthTest
```

## Install python stuff with pip

Ensure that python pip is ok:
```
sudo -H pip3 install --upgrade pip
```
and then install
```
pip install --upgrade pytest virtualenv virtualenvwrapper nose
pip install --upgrade numpy python-dateutil setuptools Cycler kiwisolver pyparsing pycairo
pip install --upgrade setuptools pyGObject
pip install --upgrade pillow matplotlib
```

## Install Jupyter Notebook, Jupyter Lab and Voila + github goodies
```
pip install --upgrade notebook
pip install --upgrade jupyterlab
pip install --upgrade voila
pip install jupyterlab_github
pip install --upgrade jupyterlab-git
```

Jupyter puts stuff in `/home.local/bin`, need to add that in `PATH`:
```
export PATH=${HOME}/.local/bin${PATH:+:${PATH}}
```
add this also in `.profile` to make it permanent.



## Install Syncthing

File synching software. 

Copied from: [Debian/Ubuntu Packages](https://apt.syncthing.net/)
```
curl -s https://syncthing.net/release-key.txt | sudo apt-key add -
echo "deb https://apt.syncthing.net/ syncthing stable" | sudo tee /etc/apt/sources.list.d/syncthing.list
sudo apt-get update && sudo apt-get install syncthing
```

## Install FATSLiM for membrane analysis


This assumes installation in `/opt`. Change if necessary and if you install in `/opt` ensure that you have the correct access rights (it is typically onwed by `root` .

```
cd /opt/git
git clone https://github.com/FATSLiM/fatslim.git
cd fatslim
sudo python3 setup.py install
```
Test that it works:
```
fatslim self-test
```

## Install MDAnalysis for trajectory analysis


**Problem:** test doesn't run, gives hundreds of error messages.

**Solution:** [](). MDAnalysis version 1.0.0 is not compatible with the latest Matplotlib (3.3). One must use an earlier version. This will be different for newever versions but for now, let's downgrade matplotlib:

```
pip uninstall matplotlib
pip install matplotlib==3.2.2
```

Now we can install MDAnalysis and run the test:

```
pip install --upgrade MDAnalysis[analysis] MDAnalysisTests MDAnalysisData pytest-xdist
pytest --disable-pytest-warnings --pyargs MDAnalysisTests --numprocesses 4
```

**NOTE:** With version 1.0.0 there are files and directories missing in the test directory. Hopefully this will be fixed in the future. I found those files in the development version and put them in the proper directory and the tests ran fine. Without doing that, there were 35 errors and 4 fails. 


## Install PyBILT for membrane analysis:


```
cd /opt/git
git clone https://github.com/LoLab-VU/PyBILT.git
pip install .
pip install scipy seaborn future
cd tests
pytest .
```
**Note**: The test may give an error regarding 'AtomGroup'. This refers to MDA. Probably a version < 1.0.0 would work.

## Install MDTraj for trajectory analysis

- Note: mdtraj not found, maybe needs a reboot.

```
pip install --upgrade mdtraj
pytest mdtraj -v 
```

## Install ProDY
Protein structural analysis.


- [ProDy home](http://prody.csb.pitt.edu/)

Install in `/opt/git` and run the tests. 

```
cd /opt/git
git clone https://github.com/prody/ProDy.git
cd ProDy
python3 setup.py build_ext --inplace --force
nosetests
```

```
export PYTHONPATH=$PYTHONPATH:$/opt/ProDy
```

Put this also in your pythonpath and `.profile`


## Install PyTIM for interface analysis:


- [PyTIM](https://github.com/Marcello-Sega/pytim)
```
pip install --upgrade pytim
```

## Install Packmol

- [Download](http://leandro.iqm.unicamp.br/packmol/versionhistory/)

```
cd /opt/git
git clone https://github.com/m3g/packmol.git
cd packmol
make
```
The executable `packmol` is in the same directory, that is, `/opt/git/packmol`

## Install pmx
- Note: Doesn't work with python >=3. If needed, create a virtual environment for pmx
- [pmx at Github](https://github.com/deGrootLab/pmx)

```
cd /opt/git
git clone https://github.com/deGrootLab/pmx pmx
cd pmx
pip install .
```

## Install DSSP:

- [DSSP at Github](https://github.com/cmbi/dssp)
  - version 2.3.0 
  
```
cd /opt/git
wget https://github.com/cmbi/dssp/archive/2.3.0.tar.gz
tar -zxvf 2.3.0.tar.gz 
cd dssp-2.3.0
./autogen.sh
./configure
make
./mkdssp
sudo make install
```
  

## Install LOOS

- [LOOS](http://grossfieldlab.github.io/loos/)
- [LOOS at Github](https://github.com/GrossfieldLab/loos)

## Install freud for trajectory analysis:

- [freud](https://github.com/glotzerlab/freud)
```
pip install --upgrade freud-analysis
```

## Diffusion analysis

- [Diffusion Analysis in MD Simulations](https://diffusion-analysis-md-simulations.readthedocs.io/en/latest/diffusion_analysis.html)
- [Clone the git](https://github.com/tylerjereddy/diffusion_analysis_MD_simulations)
- [At Zenodo](http://doi.org/10.5281/zenodo.11827)

```
cd /opt/git
git clone https://github.com/tylerjereddy/diffusion_analysis_MD_simulations.git
cd diffusion_analysis_MD_simulations
pip install .
```

## Martinez2 & Vermouth
- [Home](https://github.com/marrink-lab/vermouth-martinize)

```
pip install vermouth
pip install git+https://github.com/marrink-lab/vermouth-martinize.git#vermouth
```
 
## PyDiffusion

- [pydiffusion](https://github.com/bio-phys/pydiffusion)
- [Example notebook](https://github.com/bio-phys/pydiffusion/blob/master/example/Analysis.ipynb)

```
cd /opt/git
git clone https://github.com/bio-phys/pydiffusion.git
cd pydiffusion
sudo python3 setup.py install
```
Note: pulls the latest version of matplotlib. That, however, breaks MDAnalysis -> downgrade matplotlib
```
pip uninstall matplotlib
pip install matplotlib==3.2.2
```

## APL@Voro

- [APL@Voro](https://www.cellmicrocosmos.org/index.php/cm2-aplvoro)
- [New repository](https://bitbucket.org/martin-kern/apl-voro/src/development/)

- Note: This installs in `/opt/git/apl-voro/bin`


```
cd /opt/git
git clone https://bitbucket.org/martin-kern/apl-voro.git
cd apl-voro
qmake aplvoro.pro PREFIX=/opt/git/apl-voro/bin
make && make install
```

## PyEMMA

- [PyEMMA home](http://emma-project.org)

Installation:
```
pip install pyemma
```

## Install VMD


Download the versions of [VMD](https://www.ks.uiuc.edu/Research/vmd/) you want. Uncompress and move inside the directory. If you want to install the default with the executable called `vmd`, just jump below to configure. If you plan to install several versions, then edit the `configure` file and change the name of the executable and configure: 

```
./configure
cd src
sudo make install
```

## Other software:

## TeXMath pluguin for LibreOffice

- [TexMath](http://roland65.free.fr/texmaths/)

### WPS Office:

Probably the most MS Office compatible office software.

First, install WPS fonts:

```
cd ~/Downloads
mkdir tmp
cd tmp
git clone https://github.com/IamDH4/ttf-wps-fonts
cd ttf-wps-fonts
sudo mkdir /usr/share/fonts/wps-fonts
sudo cp *.ttf /usr/share/fonts/wps-fonts
sudo chmod 644 /usr/share/fonts/wps-fonts/*
sudo fc-cache -vfs
```

Second, [download WPS](https://www.wps.com/download). Assuming it was downloaded to `Downloads`
```
cd $USER/Downloads
sudo dpkg -i wps-offic-replace-this.deb
```

## Ulauncher

- [Ulauncher home](https://ulauncher.io/)


```
sudo add-apt-repository ppa:agornostal/ulauncher
sudo apt update 
sudo apt install ulauncher
```
## From Software Center:

- Spotify
- VLC
- Shortwave radio
- Lollypop music player
- Newsflash RSS reader
- Obs studio
- Inkscape
- Gimp
- FileZilla
- Handbrake
- Blender
- Wire
- Skype
- Zoom
- Xournal++
- audacity
- parlatype
- simple screen recorder

### Download separately

- [Jabref](https://www.jabref.org/)
- [Foxit reader](https://www.foxitsoftware.com/pdf-reader/)
- [Microsoft Teams](https://www.microsoft.com/en-ca/microsoft-365/microsoft-teams/download-app)
- [Visual Studio Code Editor](https://code.visualstudio.com/download)
