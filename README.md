#-3. Install tools
yum install -y gcc-devel g++ gcc-c++

#-2. Install deps
yum install -y libev-devel libgmp-devel lzip libev libmemcached

#-1. Download GMP
wget https://gmplib.org/download/gmp/gmp-6.1.2.tar.lz
lzip -d gmp-6.1.2.tar.lz
tar xvf gmp-6.1.2.tar
cd gmp-6.1.2
./configure
make
make install

#0. build LevelDB-Redis
git submodule init
git submodule update
make

#1. Start
ulimit -c unlimited
./ldbrp -P 9736 -D leveldb -d
