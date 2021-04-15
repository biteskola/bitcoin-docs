# Probar un PR(#19521) de Bitcoin-core usando Ubuntu 18.04.5 LTS (Bionic Beaver)
> **_IMPORTANTE:_** Si es la primera vez que compilas bitcoin en esta máquina, este punto es necesario. Este caso contrario, puedes omitirlo.

0. Pre-requisitos. Instalar berkelyDb (v4.8.30) y demas dependencias que necesita bitcoin para correr:
```bash
## permite que el software se compile desde la fuente
sudo apt-get install build-essential

## instala cliente para git y wget
sdo apt-get install git wget

## descargar BerkeleyDB desde las fuentes. La paqueteria de ubuntu tiene una version vieja.
wget http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz
## descargar y verificar el paquete fuente de BerkeleyDB 
echo '12edc0df75bf9abd7f82f821795bcee50f42cb2e5f76a6a281b85732798364ef  db-4.8.30.NC.tar.gz' | sha256sum -c
## el comando debe retornar: db-4.8.30.NC.tar.gz: OK.
## descomprimir y compilar BerkelyDB
tar -xvf db-4.8.30.NC.tar.gz
cd db-4.8.30.NC/build_unix
mkdir -p build
BDB_PREFIX=$(pwd)/build
../dist/configure --disable-shared --enable-cxx --with-pic --prefix=$BDB_PREFIX
make install
cd ../..

## Instalar las dependencias restantes
sudo apt-get install autoconf libtool pkg-config libboost-all-dev libssl-dev libprotobuf-dev protobuf-compiler libevent-dev libqt4-dev libcanberra-gtk-module qt5-default qttools5-dev-tools bsdmainutils
```

1. Clonar el repositorio donde esta el PR. Por ejemplo: ```git clone https://github.com/fjahr/bitcoin```
2. ```cd bitcoin```
3. Entrar en la rama donde esta el PR. Para este caso: ```git checkout csi-6-none-index```
4. Compilar bitcoin con el cambio del PR: 
```bash
./autogen.sh
./configure CPPFLAGS="-I${BDB_PREFIX}/include/ -O2" LDFLAGS="-L${BDB_PREFIX}/lib/" --with-gui
make
```
5. Probar el PR. Para este caso:
https://github.com/bitcoin/bitcoin/pull/19521#pullrequestreview-505535088
```bash
src/bitcoind -coinstatsindex
src/bitcoin-cli gettxoutsetinfo 'none' 1800003 true
src/bitcoin-cli gettxoutsetinfo muhash 677990
```

6. Dejar comentario con datos de la prueba realiza en el PR.
- *ACK*: Todo fue bien + pruebas realizadas y sus resultados.
- *NACK*: "Me ha fallado xxxx", "No estoy de acuerdo con zzzz", "Esto se podria mejorar de gggg manera" ...

Ejemplos de comentarios para este PR: [1](https://github.com/bitcoin/bitcoin/pull/19521#issuecomment-818288887), [2](https://github.com/bitcoin/bitcoin/pull/19521#issuecomment-819626933)
