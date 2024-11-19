### Home Scenario
##### Linux end

```bash 
# We are in Red Hat Enterprise Linux (RHEL) 9.4
# 0. Create a local library folder
export BASEPATH=/home/adrian.garcia/mylibrary/linux
export DOWNLOADPATH=/home/adrian.garcia/mylibrary/downloads
export PACKNAME="libgsl"

# 1. Download
cd $DOWNLOADPATH
wget https://ftp.gnu.org/gnu/gsl/gsl-latest.tar.gz
tar -xvzf gsl-latest.tar.gz
cd gsl-*

# 2. Install
mkdir -p $BASEPATH/$PACKNAME
./configure --prefix=$BASEPATH/$PACKNAME
make 
make install
```
##### R end - TO TEST

```R
linuxLocaLib <- "/home/adrian.garcia/mylibrary/linux"
packageName <- "libgsl"
Sys.setenv(LD_LIBRARY_PATH = file.path(linuxLocaLib,packageName,"lib"), PATH = Sys.getenv("PATH")) # "/home/adrian.garcia/.local/mylib/libgsl/lib"

## add to .Rprofile 
Sys.setenv(LD_LIBRARY_PATH = paste0("/home/adrian.garcia/.local/mylib/libgsl/lib:",Sys.getenv("LD_LIBRARY_PATH")), PATH = Sys.getenv("PATH"))


install.packages("gsl", configure.vars = "GSL_CONFIG=/home/adrian.garcia/.local/mylib/libgsl/bin/gsl-config CPPFLAGS=-I/home/adrian.garcia/.local/mylib/libgsl/include LDFLAGS=-L/home/adrian.garcia/.local/mylib/libgsl/lib")
```


### Neosome Scenario

```bash 
# We are in Red Hat Enterprise Linux (RHEL) 9.4
# 0. Create a local library folder
export BASEPATH=/mnt/neosome/adrian.garcia/mylibrary/linux
export DOWNLOADPATH=$BASEPATH/downloads
export PACKNAME="libgsl"

# 1. Download
cd $DOWNLOADPATH
wget https://ftp.gnu.org/gnu/gsl/gsl-latest.tar.gz
tar -xvzf gsl-latest.tar.gz
cd gsl-*

# 2. Install
mkdir -p $BASEPATH/$PACKNAME
./configure --prefix=$BASEPATH/$PACKNAME
make 
make install

# 0.1 



export PREFIX=$HOME$CUSTOMPATH



```


```R
Sys.setenv(LD_LIBRARY_PATH = "/home/adrian.garcia/.local/mylib/libgsl/lib", PATH = Sys.getenv("PATH"))

## add to .Rprofile 
Sys.setenv(LD_LIBRARY_PATH = paste0("/home/adrian.garcia/.local/mylib/libgsl/lib:",Sys.getenv("LD_LIBRARY_PATH")), PATH = Sys.getenv("PATH"))


install.packages("gsl", configure.vars = "GSL_CONFIG=/home/adrian.garcia/.local/mylib/libgsl/bin/gsl-config CPPFLAGS=-I/home/adrian.garcia/.local/mylib/libgsl/include LDFLAGS=-L/home/adrian.garcia/.local/mylib/libgsl/lib")
```
