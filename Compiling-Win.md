
This is a short guide on how to set up a compiling environment on Windows, and using it to compile Naev.

## Setting up your compiling environment
* Go to the [MSYS2 download page](http://sourceforge.net/projects/msys2/?source=typ_redirect) and download the installer. Run this installer and install to the default location.
* When the installation is complete, start a MinGW shell. You can do this via the start menu, or by using the bat files in your MSYS2 installation directory. There are two versions; one for 32-bit and one for 64-bit compilation. You can choose whichever one fits your system. If you do not know which one to use, use the 32-bit version.
* When the command prompt comes up for the first time, you need to install the required packages to build Naev. Simply paste the following into your command prompt (via the right mouse button) and hit enter.

For 32-bit users:
```
pacman -S mingw-w64-i686-gcc mingw-w64-i686-SDL2 mingw-w64-i686-SDL2_mixer \
mingw-w64-i686-libxml2 mingw-w64-i686-libpng mingw-w64-i686-openal \
mingw-w64-i686-libvorbis mingw-w64-i686-binutils mingw-w64-i686-freetype \
mingw-w64-i686-libzip autoconf automake-wrapper git pkgconfig make
```
For 64-bit users:
```
pacman -S mingw-w64-x86_64-gcc mingw-w64-x86_64-SDL2 mingw-w64-x86_64-SDL2_mixer \
mingw-w64-x86_64-libxml2 mingw-w64-x86_64-libpng mingw-w64-x86_64-openal \
mingw-w64-x86_64-libvorbis mingw-w64-x86_64-binutils mingw-w64-x86_64-freetype \
mingw-w64-x86_64-libzip autoconf automake-wrapper git pkgconfig make
```
When asked to proceed with the installation, press y and hit enter.

## Building
### Step 1:

Clone the git repo. Before trying to build, make sure you are in the folder of your git repo. In case it wasn't obvious, you can use the following command:

```
cd <path-to-repo>
```

With the command "pwd" you can check if you are in the right folder.

### Step 2:

First run:

```
./autogen.sh
```
Note: You should only need to do this once. And if you are using a source tarball and not using git, you do not need to run autogen.sh

### Step 3:

When ready, just run:

```
./configure
```

Followed by

```
make
```

If everything went without any errors, the compiled executable should be automatically copied to your Naev directory. If you can't find it, however, it may be in the src subdirectory. You are now ready to play!

**Tip:** If you have a multi-core CPU, you may tell make to use multiple jobs at the same time by specifying the -jn parameter, where n is the number of jobs you wish to use.

**Note:** If you start Naev from anywhere other than the MSYS command prompt, the game may complain about missing DLL files. You have these files, they are in your MSYS installation directory, under mingw32\bin or mingw64\bin, depending on which you used to compile. Simply copy all the DLLs the game asks for to the Naev directory, and you're good to go.