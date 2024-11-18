### Neosome Scenario

```bash 
# We are in Red Hat Enterprise Linux (RHEL) 9.4
# 0. Create a local library folder
export CUSTOMPATH=.local/mylib
mkdir -p $HOME/$CUSTOMPATH
export PREFIX=$HOME$CUSTOMPATH
export PACKNAME="libgsl"

# 1. Download
cd ~/$CUSTOMPATH/downloads/
wget https://ftp.gnu.org/gnu/gsl/gsl-latest.tar.gz
tar -xvzf gsl-latest.tar.gz
cd gsl-*

# 2. Install
./configure --prefix=$PREFIX/$PACKNAME
make 
make install
```


```R
Sys.setenv(LD_LIBRARY_PATH = "/home/adrian.garcia/.local/mylib/libgsl/lib", PATH = Sys.getenv("PATH"))

## add to .Rprofile 
Sys.setenv(LD_LIBRARY_PATH = paste0("/home/adrian.garcia/.local/mylib/libgsl/lib:",Sys.getenv("LD_LIBRARY_PATH")), PATH = Sys.getenv("PATH"))


install.packages("gsl", configure.vars = "GSL_CONFIG=/home/adrian.garcia/.local/mylib/libgsl/bin/gsl-config CPPFLAGS=-I/home/adrian.garcia/.local/mylib/libgsl/include LDFLAGS=-L/home/adrian.garcia/.local/mylib/libgsl/lib")
```

```