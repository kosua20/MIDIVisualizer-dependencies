# Dependencies for MIDIVisualizer

This repository is used for the automatic deployement of [MIDIVisualizer](https://github.com/kosua20/MIDIVisualizer).  
Large binary dependencies are stored as artifacts of a release.  
The repository itself contains the configurations used to generate these binaries.

Current dependencies:

* FFMPEG, static, LGPL2-only

## Instructions

### FFMPEG

FFMPEG is built as a set of static libraries using *vcpkg* on Windows, macOS and Ubuntu, with modified settings. We generate the LGPL2 version of the library with hardware encoders from Intel and Nvidia disabled, and with no debug symboles. The generated FindFFMPEG.cmake is designed specifically for use in MIDIVisualizer.

* Install *yasm*: 
  - Windows: TBA
  - macOS: use Homebrew with `brew install yasm`
  - Ubuntu: use `sudo apt-get install yasm`
* Install *vcpkg* by cloning `https://github.com/microsoft/vcpkg.git` (commit used: `f4bd64233ae875b6b3315fe4fab279335a6adf2b`).
* Install the recommended dependencies and setup *vcpkg* by running `vcpkg/bootstrap-vcpkg.{sh, bat}`.
* Replace the content of `vcpkg/ports/ffmpeg` by the content from the `ffmpeg` directory in this repository.
* For macOS, add the file `x64-osx-10-12.cmake` from this repository to the `vcpkg/triplets/` directory.
* Build FFMPEG has a set of static libraries for a 64 bits platform:
  - Windows: `vcpkg install ffmpeg:x64-windows-static`
  - macOS: `vcpkg install ffmpeg:x64-osx-10-12`
  - Ubuntu: `vcpkg install ffmpeg:x64-linux`
* Export the generated libraries and headers:
  - Windows: `vcpkg export ffmpeg:x64-windows-static --raw`
  - macOS: `vcpkg export ffmpeg:x64-osx-10-12 --raw`
  - Ubuntu: `vcpkg export ffmpeg:x64-linux --raw`
* This will put the generate package in `vcpkg-export-...`.
* Copy `vcpkg-export-.../installed/x64-.../{include, lib, share}` to a `ffmpeg` directory.
* Zip the directory, using the following output name:
  - Windows: `ffmpeg-windows-64-static-lgpl.zip`
  - macOS: `ffmpeg-osx-64-static-lgpl.zip`
  - Ubuntu : `ffmpeg-ubuntu20-64-static-lgpl.zip` or `ffmpeg-ubuntu18-64-static-lgpl.zip` depending on the version
* Upload these files in a release on this repository.
