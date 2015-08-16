# Maintainer: BlackEagle < ike DOT devolder AT gmail DOT com >
# Contributer: Tom Billiet (mouse256@ulyssis.org)

pkgname=jalbum
pkgver=12.6.4
pkgrel=1
pkgdesc="free web photo album software and photo gallery software"
url="http://jalbum.net/"
license=('custom' 'lgpl')
depends=('java-runtime')
arch=('any')
source=(
	"http://download.jalbum.net/download/$pkgver/Linux/NoVM/${pkgname}_$pkgver-1_all.deb"
	"jalbum.sh"
	"jalbum.desktop"
)

build() {
	# when using rpm source
	#bsdcpio -id < $srcdir/$pkgname-$pkgver-1.noarch.rpm

	# when using deb source
	ar vx "$srcdir/${pkgname}_$pkgver-1_all.deb"
	tar -zxf data.tar.gz

	# only take the jalbum dir, the rest we install on a different way
	mv usr/share/jalbum ./
	rm -rf usr
	#remove batfiles and java sourcefiles
	cd jalbum
	find \( -name "*.bat" -o -name "*.cmd" -o -name "*.java" -o -name "compile.sh" \) -delete

	#remove lib/sunos/windows
	rm -rf lib/{sunos,windows}

	#remove startupscript, we install one in usr/bin
	rm -f startjalbum.sh

	# remove distritbution text, it doesnt add usefull info
	rm -f distribution.txt

	#make sure no executable files are here
	chmod -R u=rwX,go=rX *
}

package() {
	install -dm755 "$pkgdir/usr/share/"
	cp -a jalbum "$pkgdir/usr/share/jalbum"

	#move licence to the correct place
	install -dm755 "$pkgdir/usr/share/licenses/"
	mv "$pkgdir/usr/share/$pkgname/license" "$pkgdir/usr/share/licenses/$pkgname"

	install -dm755 "$pkgdir/usr/share/pixmaps"
	ln -s "/usr/share/jalbum/icons/JalbumApp48.png" "$pkgdir/usr/share/pixmaps/jalbum.png"
	install -Dm644 "$srcdir/jalbum.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"
	install -Dm755 "$srcdir/jalbum.sh" "$pkgdir/usr/bin/jalbum"
}
sha256sums=('539f7d1b38bbfbda98f16d46086ba520841b449fcfcca482f521b8b87eb07b3f'
            'e1efa97077ac34ba3473cc1440f3a1427baea61e3a807d80efa6cf95c33eaf32'
            '7a059d23bd78e18681e5d960b213ef0cd2d4f37954bee40340409b459436fb33')

