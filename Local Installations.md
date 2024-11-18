### Neosome Scenario

```bash 
# We are in Red Hat Enterprise Linux (RHEL) 9.4
# 0. Create a local library folder
export CUSTOMPATH=.local/mylib
mkdir -p $HOME/$CUSTOMPATH
export PREFIX=$HOME$CUSTOMPATH
# 0.1 Temporarily set variables
export PATH=$PREFIX/bin:$PATH 
export LD_LIBRARY_PATH=$PREFIX/lib:$LD_LIBRARY_PATH 
export PKG_CONFIG_PATH=$PREFIX/lib/pkgconfig:$PKG_CONFIG_PATH 
export CPATH=$PREFIX/include:$CPATH


# 1. Download



```


```R
system("export CUSTOMPATH=.local/mylib;mkdir -p $HOME/$CUSTOMPATH;export PREFIX=$HOME$CUSTOMPATH")
system('echo "$PREFIX"')

install.packages("gsl", configure.vars = "GSL_CONFIG=/home/adrian.garcia/.local/mylib/libgsl/bin/gsl-config")

R CMD INSTALL gsl --configure-vars="CPPFLAGS=-I$PREFIX/include LDFLAGS=-L$PREFIX/lib"

# R CMD INSTALL gsl --configure-vars="CPPFLAGS=-I$PREFIX/include LDFLAGS=-L$PREFIX/lib"

```




~/.local/mylib/libgsl/include/gsl/