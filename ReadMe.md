
## Usage/Examples

Step 1
```bash
git clone --depth 1 --branch v1.1.1 https://github.com/catboost/catboost.git
cd catboost/catboost/libs/model_interface && ../../../ya make -r . --target-platform CLANG14-DARWIN-ARM64
```
CLANG14-DARWIN-ARM64 - mac m1 or your platform

P.s Versions older than v1.1.1 are no longer supported by the yamake utility see CatBoost C library

Step 2
```bash
Copy the files /usr/lib
linux: /usr/lib
osx: /usr/local/lib
```

Step 3
```bash
Set the environment variables
linux: export LD_LIBRARY_PATH=/usr/lib:$LD_LIBRARY_PATH
osx: export DYLD_LIBRARY_PATH=/usr/local/lib:$DYLD_LIBRARY_PATH
```

Step 4
```bash
go get github.com/naginnn/catgoboost
```
