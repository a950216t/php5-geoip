# Maintainer: Thore Bödecker <me [at] foxxx0 [dot] de>

pkgname=php5-geoip
_pkgbase="${pkgname#php5-}"
pkgver=1.1.1
pkgrel=2
pkgdesc="GeoIP module for php5"
arch=('i686' 'x86_64')
url="https://pecl.php.net/package/geoip"
license=('PHP')
provides=("php-geoip=${pkgver}-${pkgrel}")
depends=('php5>=5.6.17-3' 'geoip')
backup=('etc/php5/conf.d/geoip.ini')
source=("https://pecl.php.net/get/geoip-${pkgver}.tgz")
sha256sums=('b2d05c03019d46135c249b5a7fa0dbd43ca5ee98aea8ed807bc7aa90ac8c0f06')

prepare() {
    cd "${srcdir}/${_pkgbase}-${pkgver}"

    # remove broken tests
    #   geoip_setup_custom_directory() (with trailing slash) [tests/019.phpt]
    rm ./tests/019.phpt
}

build() {
    cd "${srcdir}/${_pkgbase}-${pkgver}"

    phpize5
    ./configure \
        --config-cache \
        --sysconfdir=/etc/php5 \
        --with-php-config=/usr/bin/php-config5 \
        --localstatedir=/var
    make
}

check() {
    cd "${srcdir}/${_pkgbase}-${pkgver}"
    make test NO_INTERACTION=1 REPORT_EXIT_STATUS=1
}

package() {
    cd "${srcdir}/${_pkgbase}-${pkgver}"

    make INSTALL_ROOT="$pkgdir" install
    echo ';extension=geoip.so' >geoip.ini
    install -Dm644 geoip.ini "$pkgdir/etc/php5/conf.d/geoip.ini"
}
