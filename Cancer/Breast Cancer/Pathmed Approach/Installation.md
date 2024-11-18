```bash

export rpmURL="https://yum.oracle.com/repo/OracleLinux/OL9/codeready/builder/x86_64/getPackage/gsl-devel-2.6-7.el9.x86_64.rpm"
export rpmNAME="libgsl"

mkdir -p ~/.local/mylib
export PREFIX=~/.local/mylib/$rpmNAME
export PATH=$PREFIX/bin:$PATH
export LD_LIBRARY_PATH=$PREFIX/lib:$LD_LIBRARY_PATH
export PKG_CONFIG_PATH=$PREFIX/lib/pkgconfig:$PKG_CONFIG_PATH

wget $rpmURL -P $PREFIX
# dnf --downloadonly --destdir=$PREFIX download libgsl libgsl-devel

cd $PREFIX

for rpm in *.rpm; do
    rpm2cpio "$rpm" | cpio -idmv
done


# Add final lines to ~/.bash_profile
# CAREFUL DOING THIS SEVERAL TIMES WILL ADD TOO MANY EXPORTS!
# IMPROVE TO BE AUTOMATIC

rm ~/.bash_profile
touch ~/.bash_profile
echo "# .bash_profile" >> ~/.bash_profile
echo "# Get the aliases and functions" >> ~/.bash_profile
echo "if [ -f ~/.bashrc ]; then" >> ~/.bash_profile
echo "        . ~/.bashrc" >> ~/.bash_profile
echo "fi" >> ~/.bash_profile
echo "# User specific environment and startup programs" >> ~/.bash_profile
echo "export PATH=$PWD/usr/bin:$PATH" >> ~/.bash_profile
echo "export LD_LIBRARY_PATH=$PWD/usr/lib:$PWD/usr/lib64:$LD_LIBRARY_PATH" >> ~/.bash_profile
echo "export PKG_CONFIG_PATH=$PWD/usr/lib/pkgconfig:$PWD/usr/lib64/pkgconfig:$PKG_CONFIG_PATH" >> ~/.bash_profile
# CHECK ALL FINAL THREE LINES
cat ~/.bash_profile

# CREAT CUSTOM PATH ENVIRONMENT FOR R in ~/.Rprofile

echo 'Sys.setenv(LD_LIBRARY_PATH="'$PWD'/usr/lib:'$PWD'/usr/lib64:'$LD_LIBRARY_PATH'")' >> ~/.Rprofile
echo 'Sys.setenv(PKG_CONFIG_PATH="'$PWD'/usr/lib/pkgconfig:'$PWD'/usr/lib64/pkgconfig:'$PKG_CONFIG_PATH'")' >> ~/.Rprofile
echo 'Sys.setenv(LIBRARY_PATH="'$PWD'/usr/lib:'$PWD'/usr/lib64:'$LIBRARY_PATH'")' >> ~/.Rprofile
echo 'Sys.setenv(C_INCLUDE_PATH="'$PWD'/usr/include:'$C_INCLUDE_PATH'")' >> ~/.Rprofile
echo 'Sys.setenv(CPLUS_INCLUDE_PATH="'$PWD'/usr/include:'$CPLUS_INCLUDE_PATH'")' >> ~/.Rprofile

source ~/.bash_profile


## CAREFUL WITH THIS EIDRIAN!

install.packages("gsl", configure.args = c(
  "--with-gsl-include=~/.local/mylib/libgsl/usr/include",
  "--with-gsl-config=~/.local/mylib/libgsl/usr/bin/gsl-config",
  "--with-gsl-lib=~/.local/mylib/libgsl/usr/lib64"
))

"--with-gsl-config=~/.local/mylib/libgsl/usr/bin/",
```


```bash
# SECOND WAY OF INSTALLING
## System Installation
export PREFIX
export PREFIX=~/.local/mylib
export PREFIX=~/.local/mylib/$rpmNAME

cd ~/.local/downloads/
wget https://ftp.gnu.org/gnu/gsl/gsl-latest.tar.gz
tar -xvzf gsl-latest.tar.gz
cd gsl-*

./configure --prefix=/home/adrian.garcia/.local/mylib/libgsl
make 
make install

## Check if installed
/home/adrian.garcia/.local/mylib/libgsl/bin/gsl-config --version

## Add Path to .bash_profile
export PATH=~/local/libgsl/bin:$PATH
export LD_LIBRARY_PATH=~/.local/mylib/libgsl/lib:$LD_LIBRARY_PATH

source ~/.bash_profile

```

```R
# Further stepts in R
install.packages("gsl", configure.vars = "GSL_CONFIG=/home/adrian.garcia/.local/mylib/libgsl/bin/gsl-config")

Sys.setenv(LD_LIBRARY_PATH = "/home/adrian.garcia/.local/mylib/libgsl/lib")

## check in R
Sys.setenv(LD_LIBRARY_PATH = "/home/adrian.garcia/.local/mylib/libgsl/lib")
install.packages("gsl", configure.vars = "GSL_CONFIG=/home/adrian.garcia/.local/mylib/libgsl/bin/gsl-config")

```