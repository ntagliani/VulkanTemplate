# Sample Vulkan Project using conan 2.0

This is a sample empty project that uses conan and pull some few other dependencies like GLM and GLFW to create an empty window fromw wich you can start coding.

The only expectation is to have python 3.12

## Commands to execute

Olny once 
```
pip install pipenv
```

then 
```
pipenv shell
```

to activate a shell with conan in it.

From there it's a classic conan workflow.

### Generating the visual studio solution

```
conan profile detect -force
conan install . --build=missing -s build_type=Release
conan install . --build=missing -s build_type=Debug
cd build
generators\conanbuild.bat
cd ..
cmake --preset conan-default
```
After these steps the visual studio solution can be found under the `build` subfolder.

## Notes

- DON'T USE POWERSHELL because the conan install step would fail while building in debug
- cmake won't be available before the execution of `generators\conanbuild.bat` since it will be pulled in as a tool dependency with conan and it will ignore the system available one