# Fedora KDE Setup

Ceci est mon setup pour fedora KDE 


## Sommaire

- Installation
- 1er pas
- Installation des applications
- Customization du bureau


## Installation

Tout d'abord, 
## 1er pas

Les commandes ci-dessous permettent d'installer divers packages et configurer quelques parametres essentiel à l'utilisation de l'OS.

Tout d'abord, on commence par modifier les parametres de **dnf** (le package manager de Fedora) pour augmenter sa **vitesse**. _Attention ces parametres rendront plus long la première mise à jour du système_

Ouvrir le fichier config de dnf :
```bash
sudo nano /etc/dnf/dnf.conf
```

Une fois dedans, modifier ces parametres :
```bash
fastestmirror=True
max_parallel_downloads=10
defaultyes=True
keepcache=True
```

**Sauvegarder** le fichier puis **fermer** nano avec 
[CTRL + S] et [CTRL + X]

Une fois ces parametres sauvegardés, Mettre a jour le système :

```bash
sudo dnf update
```

Puis redémarrez le système :

```bash
reboot
```

Installer **RPM Fusion** :

```bash
sudo dnf install https://mirrors.rpmfusion.org/  free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf config-manager --enable fedora-cisco-openh264
sudo rpm-ostree install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

```

Installer **Flatpack** :

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

Installer les codecs médias : 
```bash
sudo dnf groupupdate multimedia --setop="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
sudo dnf groupupdate sound-and-video
```
Et enfin, un dernier reboot :
```bash
reboot
```
## Les packages requis pour mon système

Ici je ne parlerai que des packages pour mon ordinateur en particulier donc si votre système n'a pas besoin de ces 

a partir de la g eu la flemme d'ecrire donc je met des truc random voila 
## Terminal (alacritty)

Installer alacritty 

```bash
sudo dnf install alacritty
```

Dans .config/alacritty/alacritty.toml

```bash
# $HOME/.config/alacritty/alacritty.toml
# by Rito Ghosh 2023-10-06

# Alacritty now uses TOML formatting for its config files.
# This is a simple example.

# There are the specification here: https://github.com/alacritty/alacritty/blob/master/extra/man/alacritty.5.scd
# It is not obvious how it translates to TOML. But it is extremely straightforward.

# example: WINDOW, COLORS, etc. are tables, and should be represented as [window], [colors], respectively.
# specifics of variables go under them. e.g.- look under "dynamic_padding" under-
# https://github.com/alacritty/alacritty/blob/master/extra/man/alacritty.5.scd#window
# write `dynamic_padding = true` (without backticks -`) under the table [window]
# for variables with multiple values, use "dotted keys". Like setting `padding.x = 5` under [window].
# This is simple. If not clear, do several trials and errors.

# Below is my initial set-up. The TOML homepage (https://toml.io/en/v1.0.0) was very helpful in figuring this out. 
# I put the file alacritty.toml in $HOME/.config/alacritty. However it can be kept anywhere among the places mentioned in
# https://github.com/alacritty/alacritty/tree/master#configuration

[window]

opacity = 0.6
blur = true
padding.x = 10
padding.y = 10

decorations = "Full"
decorations_theme_variant = "Light" # "Dark"

[font]

size = 12.0

# Tip: for inspiration, look for values in the source code files of your favorite VS Code themes, and use the color picker in
# Google to test colors before setting a value, or simply using an editor such as VS Code where colors are displayed in a 
# small box when a HEX is detected by the editor.

```


## Lightly

Installer Lightly
```bash
sudo dnf copr enable deltacopy/lightly-qt6
sudo dnf install lightly-qt6
```

Dans les paramètres KDE, selectionner Lightly dans Couleurs & Thèmes/Style d'applications puis redémarrer
## AlphaBlack

Dans les paramètres KDE, télécharger Breeze AlphaBlack depuis Couleurs & Thèmes/Style Plasma.
Télécharger aussi le widget depuis "ajouter des composants graphiques". redémarrer puis modifier a partir du widget.
## BetterBlur


Pour l'installer, construire le projet github

Dépendance requise pour construirea le projet
```bash
sudo dnf install git cmake extra-cmake-modules gcc-g++ kf6-kwindowsystem-devel plasma-workspace-devel libplasma-devel qt6-qtbase-private-devel qt6-qtbase-devel cmake kwin-devel extra-cmake-modules kwin-devel kf6-knotifications-devel kf6-kio-devel kf6-kcrash-devel kf6-ki18n-devel kf6-kguiaddons-devel libepoxy-devel kf6-kglobalaccel-devel kf6-kcmutils-devel kf6-kconfigwidgets-devel kf6-kdeclarative-devel kdecoration-devel kf6-kglobalaccel kf6-kdeclarative libplasma kf6-kio qt6-qtbase kf6-kguiaddons kf6-ki18n wayland-devel
```

```bash
git clone https://github.com/taj-ny/kwin-effects-forceblur
cd kwin-effects-forceblur
mkdir build
cd build
cmake ../ -DCMAKE_INSTALL_PREFIX=/usr
make
sudo make install
```

Ensuite, dans les parametres KDE, dans Gestion des fenêtres/Effets de bureau, chercher Better Blur et activer. redémarrer
## BetterBlur


Pour l'installer, construire le projet github

Dépendance requise pour construirea le projet
```bash
sudo dnf install git cmake extra-cmake-modules gcc-g++ kf6-kwindowsystem-devel plasma-workspace-devel libplasma-devel qt6-qtbase-private-devel qt6-qtbase-devel cmake kwin-devel extra-cmake-modules kwin-devel kf6-knotifications-devel kf6-kio-devel kf6-kcrash-devel kf6-ki18n-devel kf6-kguiaddons-devel libepoxy-devel kf6-kglobalaccel-devel kf6-kcmutils-devel kf6-kconfigwidgets-devel kf6-kdeclarative-devel kdecoration-devel kf6-kglobalaccel kf6-kdeclarative libplasma kf6-kio qt6-qtbase kf6-kguiaddons kf6-ki18n wayland-devel
```

```bash
git clone https://github.com/taj-ny/kwin-effects-forceblur
cd kwin-effects-forceblur
mkdir build
cd build
cmake ../ -DCMAKE_INSTALL_PREFIX=/usr
make
sudo make install
```

Ensuite, dans les parametres KDE, dans Gestion des fenêtres/Effets de bureau, chercher Better Blur et activer. redémarrer
## Règle de fenêtres

Dans les paramètres KDE, dans Gestion des fenêtres/Règles de fenêtres, il est possible de modifier beaucoup de choses pour chaque application que vous utilisez, notamment la transparence qui, combiné à Better Blur, rend très joli sur certaines fenêtres.
