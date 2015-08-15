# Contributor: Andrew Fyfe <andrew@neptune-one.net>
# Maintainer: Stefan Husmann <stefan-husmann@t-online.de>

pkgname=docbook-sgml
pkgver=4.5
pkgrel=3
pkgdesc='Document type definitions for verification of SGML data files against the DocBook rule set.'
arch=('any')
url='http://www.docbook.org/sgml/'
license=('custom')
depends=('sgml-common')
install='docbook-sgml.install'
source=("http://www.docbook.org/sgml/${pkgver}/docbook-${pkgver}.zip")
sha256sums=('8043e514e80c6c19cb146b5d37937d1305bf3abf9b0097c36df7f70f611cdf43')

build() {
	cd "$srcdir"

	local DTDDIR="usr/share/sgml/docbook-sgml-$pkgver"

	sed -i \
		-e '/ISO 8879/d' \
		-e '/gml/d' \
		docbook.cat

	# Add support for previous versions.
	cat >> docbook.cat << "EOF"

  -- Begin Single Major Version catalog changes --

PUBLIC "-//OASIS//DTD DocBook 4.4//EN" "docbook.dtd"
PUBLIC "-//OASIS//DTD DocBook 4.3//EN" "docbook.dtd"
PUBLIC "-//OASIS//DTD DocBook 4.2//EN" "docbook.dtd"
PUBLIC "-//OASIS//DTD DocBook 4.1//EN" "docbook.dtd"
PUBLIC "-//OASIS//DTD DocBook 4.0//EN" "docbook.dtd"

  -- End Single Major Version catalog changes --

EOF
}

package() {
	cd "$srcdir"

	local DTDDIR="usr/share/sgml/docbook-sgml-$pkgver"

	install -dm755 "$pkgdir/$DTDDIR"
	install -m644 docbook.cat "$pkgdir/$DTDDIR/catalog"
	install -m644 *.dtd *.mod *.dcl "$pkgdir/$DTDDIR"
}
