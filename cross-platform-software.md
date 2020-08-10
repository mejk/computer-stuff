## Cross-platform software (Linux, Windows, OSX)


Here is a list of some cross-platform software. Unless mentioned otherwise, Linux, Windows and Mac are supported.

- Linux note: If you don't have [Flatpack](https://flatpak.org/) installed, it may be a good idea install it as it provides an easy way to install and maintain the latest software versions.
  - [Install Flatpack](https://flatpak.org/setup/Ubuntu/)
  
### Word processors:

- [LibreOffice](https://www.libreoffice.org/)
  - support for LaTeX math via the fantastic `texmath` plugin and it can also use (without any plugins!) the excellent JabRef reference manager which allows for automatic updates, style changes etc. LibreOffice also has great support for svg graphics.
  - [TeXMath plugin](http://roland65.free.fr/texmaths/). Requires LaTeX installation. 
  
- [WPS Office](https://www.wps.com/). 
  - Note: On Linux, you need to install Times New Roman, Arial and symbol fonts separately. 
    - Here's how to do it: [font installation](ubuntu/word-processors-with-gui.md).
  - WPS Office has really excellent MS Word compatibility even with complex MS Word documents and Powerpoint. WPS Office (with the installation of MS fonts and the symbol fonts; instructions below) has worked perfectly for writing manuscripts without any compatibility issues.

### Reference manager
- [Jabref](https://www.jabref.org/)
  - Has BibTeX and BibLaTeX support
  - [Has browser extensions from Chrome, Firefox and Vivaldi](https://docs.jabref.org/collect/jabref-browser-extension)
  - [Can also connect directly to various LaTeX editors AND LibreOffice.](https://docs.jabref.org/advanced/resources)
  - Can import directly using  ISBN, DOI, PubMed-ID and arXiv-ID
  - On Linux: Download and install using `sudo dpkg -i`

### LaTeX

- [Sevaral options available here](https://www.latex-project.org)
- LaTeX math for presentations:
  - [EqualX](http://equalx.sourceforge.net/)
  - [LaTeXit](https://www.chachatelier.fr/latexit/). For OSX only.



### Text editors for plain text, coding, etc

- [Atom editor](https://atom.io/)
- [Visual studio code editor](https://code.visualstudio.com/)

### VNC 
- [TigerVNC](https://tigervnc.org/)
  - See: 
    - [VNC client and server installation](./computer-stuff/vnc-installation.md) and 
    - [VNC client and server basic use](computer-stuff/vnc-how-to-use.md )
### PDF readers

- [Foxit reader](https://www.foxitsoftware.com/pdf-reader/)

### Handwriting

- [Xournal++](https://github.com/xournalpp/xournalpp)

### Graphics

- [Inkscape](https://inkscape.org/)
    - Linux: Install via Software Center
    - Has LaTeX support
    - Since Inkscape creates scalable vector graphics, it great for creating conference posters
- [Gimp](https://www.gimp.org/)

### Music
- [Spotify](https://www.spotify.com). Works also on Android and iOS.
    - Linux: Install via Software Center

### Video players

- [VLC](https://www.videolan.org/)
  - Linux: Install via Software Center


### Video editing, screen recording, etc

- [Obs studio](https://obsproject.com/)
    - Linux: Install via Software Center
- [Handbrake](https://handbrake.fr/)
     - Linux: Install via Software Center
- [Blender](https://www.blender.org/https://www.blender.org/)
    - Linux: Install via Software Center

### Email
- [Thunderbird](https://www.thunderbird.net)

### Messaging, video calls, etc

- [Wire](https://wire.com).  Works also on Android and iOS.
  - Linux: Install via Software Center or [Wire from github](https://github.com/wireapp/wire-desktop/wiki/How-to-install-Wire-for-Desktop-on-Linux)
- [Telegram](https://telegram.org/). Works also on Android and iOS.
- [Skype](https://www.skype.com). Works also on Android and iOS.
    - Linux: Install via Software Center
- [Zoom](https://zoom.us/). Works also on Android and iOS.
  - Note: sometimes the Linux installation (.deb package) reports a dependency problem. While there are many ways to do that on command line, the easiest way that seems to work every time is to open the synaptic package manager and select 'Fix broken packages' from the 'Edit' menu. Command line options include
 `sudo apt update --fix-missing` and  `sudo dpkg --configure -a`. For more info on fixing problems with missing packages see [How to Fix Broken Packages in Ubuntu](https://www.maketecheasier.com/fix-broken-packages-ubuntu/)
  

### OS in OS
- [Virtualbox](https://www.virtualbox.org/)
  - Remember to install the Extension Pack to get all the features

### Math, analysis, data, coding, etc

- Molecular visualization, data analysis
  - [VMD](https://www.ks.uiuc.edu/Research/vmd/)
  - [Pymol](https://pymol.org)
  - [Avogadro](https://avogadro.cc/)
- Python
  - [Anaconda](https://www.anaconda.com/)
  - [Jupyter notebook / Jupyter lab](https://jupyter.org/)
- [Visual studio code editor](https://code.visualstudio.com/)

### Other stuff but not necesseraily free

- [Proton mail & VPN](https://protonmail.com/). Has also Android and iOS clients.
- Cloud strorage:
  - [Tresorit](https://tresorit.com). Has also Android and iOS clients.
  - [Dropbox](https://www.dropbox.com/). Has also Android and iOS clients.
  - [Owncloud](https://owncloud.org/). Has also Android and iOS clients.
    - This is probably the best solution but is more involved. 
- [Syncthing - synchronize and share files between computers](https://syncthing.net/)    
   - Syncthing is very handy, easy to set up + it's also free.
