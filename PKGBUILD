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
    '8b5ad0ef097ba17fc5bc1185264928df4aa61b6f38be8f40e97c79272f7ca5da'
    '352381b12f4d37f0c29d6e06ce1177a787faec7921bdbe07453b6943b19e5e1d'
    '880acc36d8b2a3daf13e8c65f89b018c44b4cf0f8116775b11b11f3b091d57bd'
    'fb4e0a53b383c8b8fe42e64b3cbee2dc2aaceef486cfa834bd26ab412df85ac7'
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
