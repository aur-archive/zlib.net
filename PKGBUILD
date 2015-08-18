pkgname=zlib.net
pkgver=1.04
pkgrel=3
pkgdesc="zlib compression library for .NET"
url="http://www.componentace.com/zlib_.NET.htm"
arch=(any)
license=("BSD")
depends=(mono)
makedepends=(dos2unix)
options=(!emptydirs)
source=("http://www.componentace.com/data/distr/zlib.NET_${pkgver//./}.zip"
"zlib.net.snk"
"zlib.net.pc.in")
md5sums=('b58fb31ec7552e1a13f76c5356a23468'
         '8d63feb566b98bcfe8b57235f5b1238b'
         'edd7e5b774291896d6474dab13bd8e4d')

prepare() {
	cd "$srcdir"
	find . -type f -exec dos2unix {} \;
}

build() {
	cd "${srcdir}/source"
	mcs /out:zlib.net.dll /keyfile:"$srcdir/zlib.net.snk" /debug:pdbonly /t:library `ls *.cs`
}

package() {
	cd "${srcdir}"
	install -Dm644 license.txt "$pkgdir/usr/share/licenses/zlib.net/license.txt"
	cd source
	install -Dm644 zlib.net.dll "$pkgdir/usr/lib/zlib.net/zlib.net.dll"
	install -m644 zlib.net.dll.mdb "$pkgdir/usr/lib/zlib.net/"
	find "$pkgdir" -name '*.dll' -exec gacutil -i {} -root "$pkgdir/usr/lib" \;
	install -Dm644 "$srcdir/zlib.net.pc.in" "$pkgdir/usr/lib/pkgconfig/zlib.net.pc"
	sed -i "s|@VERSION@|$pkgver|" "$pkgdir/usr/lib/pkgconfig/zlib.net.pc"
}
