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
    'rust'
)
source=(
    "${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
    'statistics-4you.service'
    'statistics-4you.sysusers'
    'statistics-4you.tmpfiles'
)
sha256sums=(
    '75daa8300a15acf9984de4c4407f1a6fe984f8a55920e4633f29ef1680953e26'
    'db2d533675483ba9ea168606bd3acd19b9c79c7fb833d8dfb313ee1118f430c6'
    '880acc36d8b2a3daf13e8c65f89b018c44b4cf0f8116775b11b11f3b091d57bd'
    '2a8947bebf9910825668ef8fd38ea2e38a7c65f00f4cb213dc43e0bd3c153b5a'
)

build() {
    cd "${pkgname}-${pkgver}"
    cargo build --release --locked
}

package() {
    cd "${pkgname}-${pkgver}"

    install -Dm 755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
    install -Dm 644 "${pkgname}.json.example" "${pkgdir}/etc/${pkgname}/${pkgname}.json"
    install -Dm 644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

    cd "${srcdir}"
    install -Dm 644 "${pkgname}.service" "${pkgdir}/usr/lib/systemd/system/${pkgname}.service"
    install -Dm 644 "${pkgname}.sysusers" "${pkgdir}/usr/lib/sysusers.d/${pkgname}.conf"
    install -Dm 644 "${pkgname}.tmpfiles" "${pkgdir}/usr/lib/tmpfiles.d/${pkgname}.conf"
}
