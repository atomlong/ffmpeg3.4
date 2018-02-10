# Maintainer: gbr <gbr@protonmail.com>
# Contributor: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>
#
# This package is a slightly modified version of:
# extra/ffmpeg2.8
# extra/ffmpeg

pkgname=ffmpeg3.4
pkgver=3.4.1
pkgrel=2
pkgdesc='Complete solution to record, convert and stream audio and video'
arch=('x86_64')
url='https://ffmpeg.org/'
license=('GPL3')
depends=('alsa-lib' 'bzip2' 'fontconfig' 'fribidi' 'glibc' 'gmp' 'gnutls' 'gsm'
         'jack' 'lame' 'libavc1394' 'libiec61883' 'libmodplug' 'libpulse'
         'libraw1394' 'libsoxr' 'libssh' 'libtheora' 'libvdpau' 'libwebp'
         'libx11' 'libxcb' 'libxml2' 'opencore-amr' 'openjpeg2' 'opus' 'sdl2'
         'speex' 'v4l-utils' 'xz' 'zlib'
         'libomxil-bellagio'
         'libass.so' 'libbluray.so' 'libfreetype.so' 'libva-drm.so' 'libva.so'
         'libva-x11.so' 'libvidstab.so' 'libvorbisenc.so' 'libvorbis.so'
         'libvpx.so' 'libx264.so' 'libx265.so' 'libxvidcore.so')
makedepends=('ladspa' 'libvdpau' 'yasm')
optdepends=('ladspa: LADSPA filters')
# https://ffmpeg.org/download.html#release_3.4
provides=('libavcodec.so=57' 'libavdevice.so=57' 'libavfilter.so=6' 'libavformat.so=57'
          'libavresample.so=3' 'libavutil.so=55' 'libpostproc.so=54' 'libswresample.so=2'
          'libswscale.so=4')
conflicts=('ffmpeg-full3.4')
source=("https://ffmpeg.org/releases/ffmpeg-${pkgver}.tar.xz"{,.asc}
        'fs56089.patch')
validpgpkeys=('FCF986EA15E6E293A5644F10B4322F04D67658D8')
sha256sums=('5a77278a63741efa74e26bf197b9bb09ac6381b9757391b922407210f0f991c0'
            'SKIP'
            '0bfcd12d1992903f21c146ae56d9ad89b52818cfb2303197ee905347c25a5427')

prepare() {
  cd ffmpeg-${pkgver}

  # https://bugs.archlinux.org/task/56089
  # Backport of http://git.videolan.org/?p=ffmpeg.git;a=commitdiff;h=a606f27f4c610708fa96e35eed7b7537d3d8f712
  patch -Np1 -i ../fs56089.patch
}

build() {
  cd ffmpeg-${pkgver}

  ./configure \
    --prefix='/usr' \
    --disable-debug \
    --incdir='/usr/include/ffmpeg3.4' \
    --libdir='/usr/lib/ffmpeg3.4' \
    --shlibdir='/usr/lib/ffmpeg3.4' \
    --disable-doc \
    --disable-static \
    --disable-stripping \
    --enable-avisynth \
    --enable-avresample \
    --enable-fontconfig \
    --enable-gmp \
    --enable-gnutls \
    --enable-gpl \
    --enable-ladspa \
    --enable-libass \
    --enable-libbluray \
    --enable-libfreetype \
    --enable-libfribidi \
    --enable-libgsm \
    --enable-libiec61883 \
    --enable-libmodplug \
    --enable-libmp3lame \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libopenjpeg \
    --enable-libopus \
    --enable-libpulse \
    --enable-libsoxr \
    --enable-libspeex \
    --enable-libssh \
    --enable-libtheora \
    --enable-libv4l2 \
    --enable-libvidstab \
    --enable-libvorbis \
    --enable-libvpx \
    --enable-libwebp \
    --enable-libx264 \
    --enable-libx265 \
    --enable-libxcb \
    --enable-libxml2 \
    --enable-libxvid \
    --enable-shared \
    --enable-version3 \
    --enable-omx

  make
}

package() {
  cd ffmpeg-${pkgver}

  make DESTDIR="${pkgdir}" install
  rm -rf "${pkgdir}"/usr/share

  find "${pkgdir}"/usr/bin -type f -exec mv {} {}3.4 \;

  install -dm 755 "${pkgdir}"/etc/ld.so.conf.d
  echo -e '/usr/lib/\n/usr/lib/ffmpeg3.4/' > "${pkgdir}"/etc/ld.so.conf.d/50-ffmpeg3.4.conf
}

# vim: ts=2 sw=2 et:
