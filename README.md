# TRAMOOC-MT
MT MODULE IN TRAMOOC PROJECT

## Information
maintainer: Tomasz Dwojak <t.dwojak@amu.edu.pl>
version: 0.1

## Installation
on Ubuntu 16.04, the server can be installed natively.

  - install required Ubuntu packages (see Dockerfile for list; if you don't use docker, also install CUDA and CUDNN)
  - install required python packages with pip:

    pip install -r requirements.txt --user

  - install amuNMT:

    git clone https://github.com/amunmt/amunmt

  - build amuNMT:

    mkdir -p amunmt/build
    cd amunmt/build
    cmake -DCMAKE_BUILD_TYPE=release .. && make -j 2 && make -j 2 python

on other Linux systems, the server can be deployed via a Docker container.

 - install Docker: https://docs.docker.com/engine/installation/
 - execute `make build`

## Models
If you want to download model, do:
```
make models
```

## Usage instructions

you can run the local server as follows (for English-German):

    ./docker-entrypoint.py en-de

you can run the server in a docker container as follows:

    docker run --rm -p 8080:8080 -v model:/model tramooc/mt_server en-de

a single server can also support multiple languages:

    docker run --rm -p 8080:8080 -v model:/model tramooc/mt_server en-de en-ru

you can also specify GPU devices which should be used by the server for each language pair;
for example, to use GPU with ID 0 and 1 for en-de, and only GPU 1 for en-ru, you should type:

    docker run --rm -p 8080:8080 -v model:/model tramooc/mt_server en-de:0,1 en-ru:1

A simple sample client is provided by `sample-client.py`. `sample-client-2.py` allows the translation of text passed via standard input.

## Supported language pairs

    - en-bg (English-Bulgarian)
    - en-cs (English-Czech)
    - en-de (English-German)
    - en-el (English-Greek)
    - en-hr (English-Croatian)
    - en-it (English-Italian)
    - en-nl (English-Dutch)
    - en-pl (English-Polish)
    - en-pt (English-Portuguese)
    - en-ru (English-Russian)
    - en-zh (English-Chinese)
