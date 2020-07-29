## Word processors with GUI: WPS Office and LibreOffice

There are also other options, but LibreOffice and WPS Office have proven to be great. WPS Office has really excellent MS Word compatibility even with complex MS Word documents and Powerpoint. WPS Office (with the installation of MS fonts and the symbol fonts; instructions below) has worked perfectly for writing manuscripts without any compatibility issues. LibreOffice tends to have some issues with Word documents that have complex formatting, but generally works great. If MS Word compatibility doesn't matter, LibreOffice has the additional feature that it has support for LaTeX math via the fantastic `texmath` plugin and it can also use (without any plugins!) the excellent JabRef reference manager which allows for automatic updates, style changes etc. LibreOffice also has great support for svg graphics. LibreOffice is my go to GUI editor for writing lecture notes for the above reasons. LibreOffice, WPS Office and Jabref may be/are available through package managers but the latest versions can be obtained from the links below: 

- [LibreOffice](https://www.libreoffice.org/). Linux, OSX, Windows
  - [Texmath](http://roland65.free.fr/texmaths/) plugin (requires LaTeX installed).  Linux, OSX, Windows
- [WPS Office](https://www.wps.com/). Linux, OSX, Windows
  - Download and install using `sudo dpkg -i`
- [Jabref](https://www.jabref.org/) reference manager. Linux, OSX, Windows
  - Compatible with BibTeX and BibLaTeX
  - Download and install using `sudo dpkg -i`


### There is one catch: Some fonts are proprietary (but there is a solution)

The only catch is that some of the common fonts, in particular the ubiqitous Times New Roman and Arial, are proprietary. The symbol font is another problem as well. This means that in Linux, they don't come with the basic system installation. They can be, however, easily installed. Here's how: 

#### ia) Microsoft fonts
In Ubuntu, use either a package manager (like synaptic) or install using command line as
```
sudo apt install ttf-mscorefonts-installer
```
- If you have problems, see also [How to install Microsoft fonts in Ubuntu](https://itsfoss.com/install-microsoft-fonts-ubuntu/)

#### ib) Symbol font for WPS Office
The above doesn't give the important (for those who need math) symbol font in WPS Office. However, it is easy to install it following the instructions below; these instructions were taken from [WPS Office fonts](https://github.com/IamDH4/ttf-wps-fonts) and tried on two Ubuntu (20.04 LTS and 18.04 LTS) systems. With these two steps (**ia** for Microsoft fonts and **ib** for the symbol font), WPS office appears to be extremely compatible with MS Word (and Powerpoint) and even the formulas typed in MS Word using the equation editor work perfectly (tested on WPS Office on Ubuntu 20.04 LTS and 18.04 LTS). 

1) Create a temporarary directory. For example `tmp` in your `Downloads` directory.
```
cd
cd Downloads
mkdir tmp
cd tmp
```

2) Get the fonts using `git`. This creates a directory `ttf-wps-fonts` and we move in there. 
  - If you don't have git installed, just do it first: `sudo apt install git` 
```
git clone https://github.com/IamDH4/ttf-wps-fonts
cd ttf-wps-fonts
```
3) Create a subdirectory for the new fonts in the font directory. Typically (at least in my Ubuntu 20.04 LTS and 18.04 LTS) the main fonts directory is at `/usr/share/fonts`. Create a subdirectory `wps-fonts` in there:
```
sudo mkdir /usr/share/fonts/wps-fonts
```
4) Copy (or move) the fonts in the new directory and change the file permissions:
```
sudo cp *.ttf /usr/share/fonts/wps-fonts
sudo chmod 644 /usr/share/fonts/wps-fonts/*
```
5) Rebuild the font cache:
```
sudo fc-cache -vfs
```
6) Remove the temporary directory if you want to. 

That's all! 

### Need even more fonts? Here's how:

#### ii) Google fonts

If you need Google fonts, it's super easy to install them using Typecatcher. Typecatcher is available through the Sofware Center or it can be installed via command line using
```
sudo apt install typecatcher
```

- See also: [Google fonts using typecatcher](https://www.linuxbabe.com/desktop-linux/install-google-web-fonts-ubuntu-16-04-typecatcher)

#### iii) Mathematica fonts
Another set of proprietary fonts are the Mathematica fonts from Wolfram. They can be installed using the command
```
sudo apt install fonts-mathematica
```
#### iv) Even more fonts:

You may also want to install some other fonts unless they are already installed:
```
sudo apt install fonts-liberation fonts-liberation2
```

### More information about fonts:
- [Ubuntu Fonts](https://itsfoss.com/install-fonts-ubuntu/)
- [How to install fonts on Ubuntu 20.04](https://linuxconfig.org/how-to-install-fonts-on-ubuntu-20-04-focal-fossa-linux)


