# Raylib Kickstart
This template repository offers a nice starting point for a simple raylib project with a plug-and-play cmakelistsfile that will automatically detect new source and header files. After creating a new repository based on this one, you should go to line 18 in [CMakeLists.txt](CMakeLists.txt) and change the name of the cmake project from RalyibKickstart.
![image](https://github.com/user-attachments/assets/a21651ab-c1e8-45de-b161-7b9792145a93)


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
    wezterm start --cwd . --always-new-process --class floating ./$(basename $(dirname $PWD))
fi
exit
```
