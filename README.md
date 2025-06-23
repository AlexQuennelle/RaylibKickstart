# Raylib Kickstart
This template repository offers a nice starting point for a simple raylib project with a plug-and-play cmakelistsfile that will automatically detect new source and header files. After creating a new repository based on this one, you should go to line 18 in [CMakeLists.txt](CMakeLists.txt) and change the name of the cmake project from RalyibKickstart.
![image](https://github.com/user-attachments/assets/a21651ab-c1e8-45de-b161-7b9792145a93)
The comment says to match the current folder(which in most cases will be the name of the repository) but it can really be anything. The reason for doing as the comment says is to allow the provided [build scripts](#how-to-build) to run the program after building.


## How To Build
First, ensure you have a C and C++ compiler (clang or msvc on Windows, clang or gcc on Linux), as well as cmake and emscripten(for web builds) installed. Optionally, you can also install raylib locally, but cmake will install it for you on a per project basis if you don't.
### Windows
```bat
@echo off
```
### Linux
To build a project created with this repository on linux, you should create a file called build.sh in the root directory of your project and add the following code:
```bash
read -p "Build type: " buildType
mkdir -p bin
if [[ "${buildType/w/W}" = "Web" ]]; then
    mkdir -p build.web
    cd build.web
    emcmake cmake -DCMAKE_BUILD_TYPE=Release -DPLATFORM=Web ..
    emmake make
    cd ..
    exit
elif [[ "${buildType^}" != "Debug" && "${buildType^} != Release" ]]; then
    buildType="Debug"
fi
mkdir -p build
cd build
cmake -DCMAKE_BUILD_TYPE="${buildType^}" .. -G "Unix Makefiles"
make
cd ..
if [[ "${buildType^}" = "Debug" ]]; then
    cd bin
    ./$(basename $(dirname $PWD))
fi
exit
```
