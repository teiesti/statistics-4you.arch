# Maintainer: Tobias Stolzmann <tobias.stolzmann@gmail.com>
pkgname=statistics-4you
pkgver=0.1.0
pkgrel=1
pkgdesc="Daemon fetching statistics from Mennekes AMTRON 4You charge points"
arch=('x86_64')
url="https://github.com/teiesti/statistics-4you"
license=('MIT')
makedepends=(
    'git'
    'rust>=1.89'
)
source=(
    "${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
    'statistics-4you.service'
)
sha256sums=(
    'SKIP'
    'SKIP'
)

build() {
    cd "${pkgname}-${pkgver}"
    cargo build --release --locked
}

package() {
    cd "${pkgname}-${pkgver}"

    install -Dm 755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
    install -Dm 644 "${pkgname}.json.example" "${pkgdir}/etc/${pkgname}/${pkgname}.json"
    install -Dm 644 "${pkgname}.service" "${pkgdir}/usr/lib/systemd/system/${pkgname}.service"
    install -Dm 644 "${pkgname}.sysusers" "${pkgdir}/usr/lib/sysusers.d/${pkgname}.conf"
    install -Dm 644 "${pkgname}.tmpfiles" "${pkgdir}/usr/lib/tmpfiles.d/${pkgname}.conf"
    install -Dm 644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
