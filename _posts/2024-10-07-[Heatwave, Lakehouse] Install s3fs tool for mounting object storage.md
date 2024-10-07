---
layout: post
---

## 1. install pre-requisite software in os

```
yum install automake
yum install pkg-config
yum install fuse-devel
yum install libcurl-devel libxml2-devel gcc-c++
yum install openssl gnutls nss
```

## 2. install s3fs software using mount tool for object storage bucket

- source url 
  - https://github.com/s3fs-fuse/s3fs-fuse

- installation procedures
  
```
git clone https://github.com/s3fs-fuse/s3fs-fuse.git
cd s3fs-fuse
./autogen.sh
./configure
```
```
make
sudo make install
```

## 3. Set-up authentification of object storage

- select User Settings in oci account
  - Click Customer Secret Keys, and then click Generate Secret Key.

- Enter your credentials in a ${HOME}/.passwd-s3fs file and set owner-only permissions:
  
```
echo ACCESS_KEY_ID:SECRET_ACCESS_KEY > ${HOME}/.passwd-s3fs
chmod 600 ${HOME}/.passwd-s3fs
```

## 4. mount object storage bucket in os  
```
sudo /usr/local/bin/s3fs genai /genai -o endpoint=ap-chuncheon-1 -o passwd_file=${HOME}/.passwd-s3fs -o url=https://<<namespace>>.compat.objectstorage.ap-chuncheon-1.oraclecloud.com/ -onomultipart -o use_path_request_style
```
