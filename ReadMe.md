
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
go install github.com/naginnn/cgoboost
```

Step 5
Usage
```bash
func main() {

	model, err := cgoboost.Load(
		"model.cbm")
	if err != nil {
		log.Println(err)
	}
	defer func(model *cgoboost.Model) {
		err = model.Free()
		if err != nil {

		}
	}(model)

	// get metadata from model
	var param cgoboost.ClassParams
	err = model.GetMetaData("class_params", &param)
	if err != nil {
		return
	}
	floats := [][]float32{{
		5.0, 0.0, 0.0, 1973.0, 0.0,
		2048755.0, 9.0, 12.0, 431.0, 21103.0,
		21088.0, 15.0, 0.0, 0.0, 0.0,
		2048929.0, 22728486.0, 12.0, 0.0, 0.0,
		22289201.0, 0.0, 42875644.0, 58761330.0,
		45063584.0, 0.0, 0.0}}
	cats := [][]string{}
	prediction, err := model.CalcModelPredictionProba(floats, cats)
	fmt.Println("result_proba", prediction)
	fmt.Println(param.ClassToLabel)
	fmt.Println(param.ClassNames)
	fmt.Println(model.GetFloatFeaturesCount())
	fmt.Println(model.GetCatFeaturesCount())
	fmt.Println(model.GetDimensionsCount())
}

```

