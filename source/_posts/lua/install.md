2018.09.18


```sh
# http://lua.2524044.n2.nabble.com/does-not-compile-td7680031.html
# https://askubuntu.com/questions/194523/how-do-i-install-gnu-readline
sudo apt-get install libreadline6 libreadline6-dev

curl -R -O http://www.lua.org/ftp/lua-5.3.5.tar.gz
tar zxf lua-5.3.5.tar.gz
cd lua-5.3.5
make linux test
```