# Maintainer: Frank Cringle <fdc-git@t-online.de>
pkgname=hid-mapper-pkg
pkgver="r17.2a80972"
pkgrel=1
pkgdesc="Handler for problematic USB HID devices, such as IR remotes"
url="https://github.com/s-leroux/hid_mapper"
arch=('i686' 'x86_64' 'armv7h')
license=('GPL')
depends=(gcc-libs)
makedepends=('git')
backup=()
install="$pkgname.install"
source=("git+https://github.com/s-leroux/hid_mapper.git"
	dspinellis.patch
	make-fixes.patch
	60-hid-mapper.rules
	70-zotac-ir.hwdb
	hid-mapper@.service
	vdr.map
	remote.conf)
noextract=()
md5sums=('SKIP'
         '814cecc9d10e36859473d5080fc03128'
         '0e54ab4f273478e597d0551e03674f7b'
         '794cca783d566efa8e9c43107fb6012a'
         '25a6fea3422d9204829266b282a9a9c3'
         'c1ad4f8c9b89ab74cb22ed56800dad23'
         'e9a7d300b49fb0c8b01803fa1ca308a1'
         '7fe79450f03ce0e31bb7d0b79bf0383b')

pkgver() {
  cd "${srcdir}/hid_mapper"
  printf \"r%s.%s\" $(git rev-list --count HEAD) $(git rev-parse --short HEAD)
}

prepare() {
  cd "${srcdir}/hid_mapper"
  patch -p1 -i "$srcdir/dspinellis.patch"
  patch -p1 -i "$srcdir/make-fixes.patch"
  sed -i -e 's/CPPFLAGS/CXXFLAGS/g' Makefile
}

build() {
  cd "${srcdir}/hid_mapper"
  make 
}

package() {
  cd "${srcdir}/hid_mapper"
  install -D -m755 hid_mapper "${pkgdir}/usr/bin/hid_mapper"
  install -D -m644 COPYRIGHT ${pkgdir}/usr/share/doc/hid-mapper/copyright
  install -D -m644 CHANGELOG ${pkgdir}/usr/share/doc/hid-mapper/changelog
  install -D -m644 README ${pkgdir}/usr/share/doc/hid-mapper/README
  mkdir -p ${pkgdir}/usr/share/hid-mapper
  cp "${srcdir}/vdr.map" maps/* ${pkgdir}/usr/share/hid-mapper
  install -D -m644 "${srcdir}/remote.conf" ${pkgdir}/usr/share/doc/hid-mapper/remote.conf
  install -D -m644 "${srcdir}/60-hid-mapper.rules" ${pkgdir}/usr/lib/udev/rules.d/60-hid-mapper.rules
  install -D -m644 "${srcdir}/70-zotac-ir.hwdb" ${pkgdir}/usr/lib/udev/hwdb.d/70-zotac-ir.hwdb
  install -D -m644 "${srcdir}/hid-mapper@.service" ${pkgdir}/usr/lib/systemd/system/hid-mapper@.service
}
