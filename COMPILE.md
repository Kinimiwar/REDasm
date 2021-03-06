## Requirements for all platforms
* CMake >= 3.10
* Qt >= 5.9 LTS
* C++11 capable compiler
  * GCC on Linux
  * Visual Studio 2017 on Windows
* git
****
### Building REDasm on Windows
Open a Command prompt and execute:
```bash
call "C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Auxiliary\Build\vcvars64.bat"
set QTCREATOR=C:\Qt\Tools\QtCreator\bin
set QTDIR=C:\Qt\5.9\msvc2017_64\bin # Change this to your Qt Version
set PATH=%QTDIR%;%QTCREATOR%;%PATH%

git clone --recursive https://github.com/REDasmOrg/REDasm.git
cd REDasm
mkdir build
cd build
cmake -G "NMake Makefiles" -DCMAKE_BUILD_TYPE=Release ..
jom -jN # Or 'nmake' N=number of cores (-j4, -j8, ...)

# Extra steps for deploying REDasm in a separate folder called 'deploy'
mkdir deploy
xcopy LibREDasm.dll deploy
xcopy REDasm.exe deploy
cd deploy
windeployqt --release .

# Clone REDasm-Database
git clone https://github.com/REDasmOrg/REDasm-Database.git database
rmdir /S /Q database\.git
```

### Building REDasm on Linux
Open a Terminal window and execute:
```bash
git clone --recursive https://github.com/REDasmOrg/REDasm.git
cd REDasm
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make -jN # N=number of cores (-j4, -j8, ...)

# Extra steps for deploying REDasm in a separate folder called 'deploy'
mkdir deploy
cp LibREDasm.so deploy/
cp REDasm deploy/

# Clone REDasm-Database
cd deploy
git clone https://github.com/REDasmOrg/REDasm-Database.git database
rm -rf database/.git
```
