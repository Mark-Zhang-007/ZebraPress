# Go Samples

## 1. install go

### windows with default path: c:\go

## 2. create directory as your workspace

### mkdir c:\goworkspace

## 3. setup environment variables

### GOPATH= c:\goworkspace

## 4. create src directory

### mkdir c:\goworkspace\src

## 5. create package directory

### mkdir c:\goworkspace\src\myPKG

## 6. create single go package file

### pkg1.go

#### package {common package name}
#### var Name = "Variable1"

## 7. install/compile package file

### 1) cd c:\goworkspace\src
### 2) go install {common package name}

## 8. package directory will be generatd under path:

#### c:\goworkspace\pkg\\{go installation version}\\{common package name}.a

## 9. create new go file and import new package

```md
package main
import(
   "fmt"
   "{common package name}"
)

func main(){
   fmt.Println({common package name}.variable)
}
```

## 10. summary

#### can create source code under c:\goworkspace\src directly or sub-folder

#### and import generated common package