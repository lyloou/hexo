2018-12-21 10:12:40

https://www.videolan.org/developers/libdvbcsa.html

export LD_LIBRARY_PATH=/usr/local/lib
sudo ldconfig -v

```sh
# configure.ac
# Makefile.am
git clone https://code.videolan.org/videolan/libdvbcsa.git
cd libdvbcsa

sudo apt-get install automake autoconf
sudo apt-get install libtool
autoreconf -i
./configure
make
make install
```

https://www.cnblogs.com/bugutian/p/5560548.html
http://www.51cos.com/?p=1649