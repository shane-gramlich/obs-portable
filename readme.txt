#/////////////////////////////////////////////////
# Information
#/////////////////////////////////////////////////
#  -OBS Studio
#  -Ubuntu 16.04

#/////////////////////////////////////////////////
# Dependencies
#/////////////////////////////////////////////////
sudo apt-get install build-essential pkg-config cmake git checkinstall libx11-dev libgl1-mesa-dev libpulse-dev libxcomposite-dev libxinerama-dev libv4l-dev libudev-dev libfreetype6-dev libfontconfig-dev qtbase5-dev libqt5x11extras5-dev libx264-dev libxcb-xinerama0-dev libxcb-shm0-dev libjack-jackd2-dev libcurl4-openssl-dev libavcodec-dev libavfilter-dev libavdevice-dev libfdk-aac-dev git-core

#/////////////////////////////////////////////////
# Clone OBS Source
#/////////////////////////////////////////////////
cd ~ && git clone -b 'master' 'https://github.com/jp9000/obs-studio.git' ~/'Downloads/obs-src' && sync

#/////////////////////////////////////////////////
# Compile
#/////////////////////////////////////////////////
mkdir -p ~/'Downloads/obs-src/build' && cd ~/'Downloads/obs-src/build' && cmake -DUNIX_STRUCTURE=1 -DCMAKE_INSTALL_PREFIX=/usr .. && make -j4 && sudo checkinstall --pkgname=obs-studio --fstrans=no --backup=no --pkgversion="$(date +%Y%m%d)-git" --deldoc=yes && sync

#/////////////////////////////////////////////////
# Portable
#/////////////////////////////////////////////////
mkdir -p ~/'Downloads/obs-src/build-portable' && cd ~/'Downloads/obs-src/build-portable' 
cmake -DUNIX_STRUCTURE=0 \
  -DCMAKE_INSTALL_PREFIX="${HOME}/obs-studio-portable" ..
make -j4 && make install

#/////////////////////////////////////////////////
# Uninstall
#/////////////////////////////////////////////////
rm -R ~/'Downloads/obs-src' && sync
sudo apt-get remove 'obs-studio'

#/////////////////////////////////////////////////
# Settings
#/////////////////////////////////////////////////
# -1500 Video Bitrate
# -Screen Capture on main monitor
# -Microphone volume about 1/4th volume
