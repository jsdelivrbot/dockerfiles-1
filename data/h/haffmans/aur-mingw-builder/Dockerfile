# Arch Linux based image for MingW32 package building.  
#  
# This image is focused at building AUR mingw-w64 packages. It uses yaourt and
a package list  
# to build the packages. All packages can be saved to a custom repository.  
#  
# See README.md for details.  
FROM base/archlinux:latest  
MAINTAINER Wouter Haffmans <wouter@simply-life.net>  
  
# Update base system  
RUN pacman -Sy --noconfirm --noprogressbar archlinux-keyring \  
&& pacman-key --populate \  
&& pacman -Su --noconfirm --noprogressbar pacman \  
&& pacman-db-upgrade \  
&& pacman -Su --noconfirm --noprogressbar ca-certificates \  
&& trust extract-compat \  
&& pacman -Syyu --noconfirm --noprogressbar \  
&& (yes | pacman -Scc)  
  
RUN echo "[multilib]" >> /etc/pacman.conf \  
&& echo "Include = /etc/pacman.d/mirrorlist" >> /etc/pacman.conf \  
&& pacman -Sy --noprogressbar  
  
# Add some useful devel packages to the base system  
RUN pacman -S --noconfirm --noprogressbar --needed \  
base-devel \  
ninja \  
git \  
subversion \  
yajl \  
mingw-w64-toolchain \  
python2 \  
python \  
cmake \  
libpng \  
dos2unix \  
libxml2 \  
setconf \  
jsoncpp \  
boost-libs \  
&& (yes | pacman -Scc)  
  
# Create build user...  
RUN useradd -m -d /build -u 1000 -U -G users,tty -s /bin/bash build  
ADD sudoers-99_yaourt /etc/sudoers.d/99_yaourt  
ADD yaourtrc /etc/yaourtrc  
ADD makepkg.conf /etc/makepkg.conf  
  
# Prepare build dir: add update scripts and key list  
# (packages.txt will be generated by update-packages below)  
ADD update.sh \  
update-packages.sh \  
pubkeys.txt \  
/build/  
  
RUN mkdir -p /build/repo \  
&& chown -R build:build /build \  
&& chmod +x /build/update.sh \  
&& chmod +x /build/update-packages.sh  
  
USER build  
ENV HOME=/build  
WORKDIR /build/  
  
# Install yaourt  
RUN cd /tmp \  
&& git clone https://aur.archlinux.org/package-query.git \  
&& cd package-query \  
&& makepkg -si --noconfirm \  
&& cd .. \  
&& rm -rf package-query \  
&& git clone https://aur.archlinux.org/yaourt.git \  
&& cd yaourt \  
&& makepkg -si --noconfirm \  
&& cd .. \  
&& rm -rf yaourt  
  
# Update package list  
RUN /build/update-packages.sh  
  
VOLUME /build  

