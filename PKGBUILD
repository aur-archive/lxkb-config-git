# Contributor: Yarema aka Knedlyk <yupadmin@gmail.com>
pkgname=lxkb-config-git
pkgver=20130121
pkgrel=1
pkgdesc="Lxkb-config  is a program used to configure keyboard for LXDE."
arch=('i686' 'x86_64')
url="http://lxde.org/"
license=('GPL')
depends=('gtk2>=2.12.0' 'xkeyboard-config' 'libxml2')
makedepends=('git')
conflicts=('lxkb-config')
provides=('lxkb-config')
groups=('lxde-git')
source=()
md5sums=()

_gitroot='https://github.com/azubieta/lxkb_config.git'
_gitname='lxkb-config'

build() {
  cd "${srcdir}"

  if [ -d "${srcdir}/${_gitname}" ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi
  msg "GIT checkout done or server timeout. Preparing sources..."

  [ -d "${srcdir}/${_gitname}-build" ] && rm -rf "${srcdir}/${_gitname}-build"
  cp -r "${srcdir}/${_gitname}" "${srcdir}/${_gitname}-build"
  cd "${srcdir}/${_gitname}-build"

  msg "Starting make..."
  ./bootstrap || return 1
  ./configure --prefix=/usr \
              --sysconfdir=/etc \
              --localstatedir=/var || return 1

  make || return 1
  make DESTDIR="$pkgdir" install || return 1
#  mv $pkgdir/usr/share/applications/keyboard.desktop $pkgdir//usr/share/applications/keyboard-lxde.desktop 
}
