# Merged with official ABS calligra PKGBUILD by João, 2021/05/30 (all respective contributors apply herein)
# Maintainer: João Figueiredo & chaotic-aur <islandc0der@chaotic.cx>
# Maintainer: Solomon Choina <shlomochoina@gmail.com

pkgname=calligra-git
pkgdesc="A set of applications for productivity and creative usage"
pkgver=3.3.89_r102346.ga0726e34
pkgrel=1
arch=($CARCH)
url='https://www.calligra-suite.org/'
license=(FDL1.2 GPL2 LGPL)
depends=(cauchy gcc-libs glibc gsl imath kactivities5 kcontacts5 kcoreaddons5 kdelibs4support-git kdiagram5 kcmutils5 kinit-git knotifyconfig5 kross-git kwidgetsaddons5 libodfgen libspnav poppler-qt5 qca-qt5-git qt5-base)
makedepends=(git boost eigen extra-cmake-modules-git kcalendarcore5 kdesignerplugin-git kdoctools5 libakonadi5 libetonyek libgit2 libvisio libwpg libwps marble-common-git pstoedit vc)
optdepends=('kirigami2-git: for Calligra Gemini'
            'libetonyek: Apple Keynote import filter'
            'libgit2: Calligra Gemini git plugin'
            'libvisio: Microsoft Visio import filter'
            'libwpg: Corel WordPerfect Graphics image importer'
            'libwps: Microsoft Works file word processor format import'
            'poppler: PDF to SVG filter'
            'pstoedit: EPS to SVG filter'
            'qt5-quickcontrols: for Calligra Gemini'
            'qt5-webengine: for Calligra Gemini')
conflicts=(${pkgname%-git})
provides=(${pkgname%-git})
source=("git+https://github.com/KDE/${pkgname%-git}.git")
sha256sums=('SKIP')

pkgver() {
  cd ${pkgname%-git}
  _ver="$(grep -m1 'set(CALLIGRA_VERSION_STRING' CMakeLists.txt | cut -d '"' -f2 | tr - .)"
  echo "${_ver}_r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}

build() {
  cmake -B build -S ${pkgname%-git} \
    -DBUILD_TESTING=OFF
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build

# Remove utterly broken thumbnailers
  rm "$pkgdir"/usr/lib/qt/plugins/calligra*thumbnail.so
}
