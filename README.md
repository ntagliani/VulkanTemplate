# Sample Vulkan Project using conan 2.0

This is a sample empty project that uses conan and pull some few other dependencies like GLM and GLFW to create an empty window fromw wich you can start coding.

## Requirements

- Python 3.12
- cmake (this is needed only if you want to locally build debug packages, see note below)

## Commands to execute

Olny once 
```
pip install pipenv
```

then to locally install conan
```
pipenv install
```
followed by
```
pipenv shell
```

to activate a shell with conan in it. You can verify if it works by running `conan version`.

From there it's a classic conan workflow.

### Generating the visual studio solution

```
conan profile detect
conan install . --build=missing
cd build
generators\conanbuild.bat
cd ..
cmake --preset conan-default
```
> [!NOTE]
> This will generate the visual studio solution that builds only in release mode. 

If you want to be able to build both release and debug follow the next steps instead
```
conan profile detect
conan install . --build=missing -s build_type=Release
conan install . --build=missing -s build_type=Debug
cd build
generators\conanbuild.bat
cd ..
cmake --preset conan-default
```

> [!NOTE]
conan center provides most of the packages for release builds. Invoking `--build=missing` for a `build_type=Debug` might cause compilations to be triggered on the local machine and thus a system cmake might be required.


After these steps the visual studio solution can be found under the `build` subfolder.

## Notes

- Building using powershell it is possible but it requires to add `--conf=tools.env.virtualenv:powershell=True` to your conan install commands or to your profile and allowing the execution of scripts from files ( https://go.microsoft.com/fwlink/?LinkID=135170)
- If you don't install cmake at system level it won't be available before the execution of `generators\conanbuild.bat` since it will be pulled in as a tool dependency with conan