This is a short guide to compiling Naev on *nix-based systems.

# Dependencies
First install the Naev dependencies. They should be fairly common on most systems. They are:

* SDL
* SDL_mixer
* OpenGL
* libxml 2
* Freetype 2
* libpng 1.2
* OpenAL
* libvorbis
* binutils
* libzip

## Debian Wheezy, Ubuntu 14.04 and Newer
Since 0.6.0-beta2, Naev's official binaries use SDL 2, available since Ubuntu 14.04 and Debian Wheezy (via wheezy-backports).

Dependencies for SDL 2 versions of Naev can be installed with:

```sh
apt-get install libsdl2-2.0-0 libsdl2-image-2.0-0 libgl1-mesa-dri \
  libxml2 libfreetype6 libpng-dev libopenal1 libvorbis0a libzip2
```

For compiling, you'll need the additional:

```sh
apt-get install build-essential automake libsdl2-dev libsdl2-image-dev \
  libgl1-mesa-dev libxml2-dev libfreetype6-dev libpng12-dev libopenal-dev \
  libvorbis-dev binutils-dev libzip-dev libiberty-dev autopoint intltool \
  autoconf-archive libfontconfig1-dev itstool
```

## Gentoo
sdl-mixer requires vorbis support

```sh
emerge media-libs/libsdl media-libs/sdl-image media-libs/sdl-mixer virtual/opengl\
  dev-libs/libxml2 media-libs/freetype media-libs/libpng media-libs/openal\
  media-libs/libvorbis sys-devel/binutils dev-libs/libzip
```

## Arch
First make sure you have autotools and pkg-config installed:

```sh
pacman -S --needed automake autoconf pkg-config
```

Then, install the dependencies:

```sh
pacman -S --needed sdl2 sdl2_image sdl2_mixer libxml2 freetype2 libpng libvorbis libzip
```

Or, if you would rather build with SDL 1.2, use the following:

```sh
pacman -S --needed sdl sdl_image sdl_mixer libxml2 freetype2 libpng libvorbis libzip
```
## Fedora and Other RHEL-based Distributions
First, make sure you have make, automake and gcc installed:

```sh
sudo dnf install make automake gcc intltool
```

To compile and build Naev you'll need to install the following packages:

```sh
sudo dnf install SDL2-devel SDL2_image-devel SDL2_mixer-devel libxml2-devel \
  fontconfig-devel libpng12-devel openal-soft-devel libvorbis-devel binutils-devel \
  libzip-devel gettext-devel mesa-libGLU-devel itstool
```

For running the compiled binary, you'll need the following packages installed:

```sh
sudo dnf install SDL2 SDL2_mixer SDL2_image mesa-libGLU libxml2 \
  fontconfig libpng12 openal-soft libvorbis libzip 
```

## Compiling
First, clone the Git repository.

If using Git, create the configuration scripts with:

```sh
./autogen.sh
```

Now you get to configure Naev. Usually the defaults should be adequate so run:

```sh
./configure
```

And proceed to compile with:

```sh
make
```

If all went well you should see something like:

```
$ make
Making all in lib
Making all in csparse
  CC    cs_add.o
  CC    cs_amd.o
  ...
  CC    naev
Making all in utils
Making all in pack
  CC    main.o
  CC    md5.o
  CC    pack.o
  CC    pack
$
```

Indicating the binary was built. Now you can run naev with:

```sh
./naev
```

Enjoy!