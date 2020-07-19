# Dependencies for MIDIVisualizer

This repository is used for the automatic deployement of [MIDIVisualizer](https://github.com/kosua20/MIDIVisualizer).  
Large binary dependencies are stored as artifacts of a release.  
The repository itself contains the configurations used to generate these binaries.

Current dependencies:

* FFMPEG, static, LGPL2-only

## Instructions

### FFMPEG

FFMPEG is built using *vcpkg* on Windows, macOS and Ubuntu, with modified settings. 

* Install *yasm*: 
  - Windows: TBA
  - macOS: use Homebrew with `brew install yaml`
  - Ubuntu: use `sudo apt-get install yaml`
* Install *vcpkg* by cloning `https://github.com/microsoft/vcpkg.git` (commit used: `f4bd64233ae875b6b3315fe4fab279335a6adf2b`).
* Install the recommended dependencies and setup *vcpkg* by running `vcpkg/bootstrap.{sh, bat}`.
* Replace the content of `vcpkg/ports/ffmpeg` by the content from the `ffmpeg` directory in this repository.
* Build and export FFMPEG has a set of static libraries for a 64 bits platform:
  - Windows: `vcpkg export ffmpeg:x64-windows-static --raw`
  - macOS: `vcpkg export ffmpeg:x64-osx --raw`
  - Ubuntu: `vcpkg export ffmpeg:x64-linux --raw`
* This will put the generate package in `vcpkg-export-...`.
* Copy `vcpkg-export-.../installed/x64-.../{include, lib, share}` to a `ffmpeg` directory.
* Zip the directory, using the following output name:
  - Windows: `ffmpeg-windows-64-static-lgpl.zip`
  - macOS: `ffmpeg-osx-64-static-lgpl.zip`
  - Ubuntu: `ffmpeg-linux-64-static-lgpl.zip`
* Upload these files in a release on this repository.
