# Maintainer: Azote <azote@outlook.jp>
pkgname=sysrq-on-shutdown
pkgver=1.0.0
pkgrel=1
pkgdesc="Systemd service to enable full SysRq keys during shutdown and reboot"
arch=('any')
url="https://github.com/azotegwei/sysrq-on-shutdown"
license=('CC0-1.0')
depends=('systemd')
install="$pkgname.install"
source=("$pkgname.service"
        "$pkgname.8")
sha256sums=('d3311f9dc62b6edd9872493a6f4469097a7c11ce8e36a89be8b466b418cedf20'
            '30cfcfd6ac2613a6ddc8a526dcf92868a14226550c681f25f0c0d0b656bf62c1')

package() {
  install -Dm644 "$srcdir/$pkgname.service" "$pkgdir/usr/lib/systemd/system/$pkgname.service"
  install -Dm644 "$srcdir/$pkgname.8" "$pkgdir/usr/share/man/man8/$pkgname.8"
}
