# Maintainer: loserMcloser <reebydobalina@gmail.com>

_gitname=plymouth-random-theme
pkgname="$_gitname-git"
pkgver=r2.3e195d4
pkgrel=1
pkgdesc="Chooses a random plymouth theme on each shutdown for the next boot."
arch=('any')
url="https://github.com/loserMcloser/$_gitname"
license=('CC0')
depends=('mkinitcpio' 'plymouth' '3cpio')
source=("git+https://github.com/loserMcloser/$_gitname.git")
md5sums=('SKIP')
backup=('etc/plymouth/random-theme.exclude')

pkgver() {
	cd "$srcdir/$_gitname"
	echo "r$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

package() {
	cd "$srcdir/$_gitname"
	install -Dm755 plymouth-random-theme ${pkgdir}/usr/bin/plymouth-random-theme
	install -Dm644 plymouth-random-theme.service ${pkgdir}/usr/lib/systemd/system/plymouth-random-theme.service
	install -Dm644 random-theme.exclude ${pkgdir}/etc/plymouth/random-theme.exclude
}
