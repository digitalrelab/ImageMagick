ImageMagick
===========

Digital Relab Version

## Setup
To get started setup your development repo as such:
```bash
git clone git@github.com:digitalrelab/ImageMagick.git
cd ImageMagick
git remote add upstream https://github.com/ImageMagick/ImageMagick.git
git remote -v
```

## Pulling from Upstream
To pull `upstream/master` changes into `origin/master` branch:
```bash
git fetch --all
git checkout master
git merge upstream/master
```

## Development
```bash
git checkout digitalrelab
git rebase origin/master
```

## Building
```bash
docker run --rm -it ubuntu:16.04
apt-get update
apt-get install --no-install-recommends \
                ca-certificates \
                git \
                curl \
                zip \
                p7zip-full \
                build-essential \
                checkinstall \
                libperl-dev \
                libautotrace-dev \
                libopenjp2-7-dev \
                libwebp-dev \
                libfftw3-dev \
                liblcms2-dev \
                liblcms2-utils \
                liblcms2-2 \
                libpango1.0-dev \
                libgs-dev \
                ghostscript \
                libraw-dev \
                ufraw \
                ufraw-batch \
                dcraw

cd /usr/local/src
git clone https://github.com/FLIF-hub/FLIF.git
cd FLIF
git checkout v0.3
# manually edit src/Makefile to set prefix to /usr
make install-dev
checkinstall make flif
cd ../..

git clone https://github.com/ImageMagick/ImageMagick.git
cd ImageMagick
git checkout 7.0.6-4
./configure --prefix=/usr \
            --enable-static=no \
            --enable-shared=yes \
            --with-modules=yes \
            --enable-delegate-build \
            --with-quantum-depth=16 \
            --enable-hdri=yes \
            --with-bzlib=yes \
            --with-autotrace=yes \
            --with-djvu=yes \
            --with-dps=no \
            --with-fftw=yes \
            --with-flif=yes \
            --with-fpx=no \
            --with-fontconfig=yes \
            --with-freetype=yes \
            --with-gslib=yes \
            --with-gvc=yes \
            --with-jbig=yes \
            --with-jpeg=yes \
            --with-lcms=yes \
            --with-lqr=yes \
            --with-ltdl=yes \
            --with-lzma=yes \
            --with-magick-plus-plus=yes \
            --with-openexr=yes \
            --with-openjp2=yes \
            --with-perl=yes \
            --with-png=yes \
            --with-raqm=no \
            --with-raw=yes \
            --with-rsvg=yes \
            --with-tiff=yes \
            --with-webp=yes \
            --with-wmf=yes \
            --with-x=yes \
            --with-xml=yes \
            --with-zlib=yes
checkinstall
# clean up version stuff etc
```

## Vendoring
Pull files from `s3://artifacts.digitalrelab.com`
