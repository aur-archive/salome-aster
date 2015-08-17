# Maintainer: Michele Mocciola <mickele>

pkgname=salome-aster
pkgver=2014.2
pkgrel=2
pkgdesc="Generic platform for Pre and Post-Processing for numerical simulation - ASTER Module"
url="http://www.code-aster.org/V2/spip.php?article295"
depends=('salome-gui>=7.4.0' 'salome-gui<7.5.0' 'aster' 'astk')
makedepends=()
arch=('i686' 'x86_64')
license=('LGPL')
source=("https://bitbucket.org/code_aster/salome-codeaster/get/${pkgver}.tar.gz" "http://www.code-aster.org/FICHIERS/SALOME-MECA-2014.2-LGPL-1.tgz" ${pkgname}.profile)

_source=code_aster-salome-codeaster-3f5aee03a544
_installdir=/opt/salome/aster

prepare() {
  # extracts salome_meca (we need salome_pyutils)
  cd "$srcdir"
  tail --lines=+597 SALOME-MECA-2014.2-LGPL.run > extracted.tar.gz
  tar xzf extracted.tar.gz

  # python -> python2
  cd "$srcdir/$_source"
  for _FILE in profile_init.sh salome/tests/test_run_aster_solver.py salome/aster_gui_tests.py tests/gui-supervision/aster-solver tests/gui-supervision/astk-tasks tests/gui-supervision/salome-supervisor.py
  do
    sed -e "s|python|python2|" -i ${_FILE}
  done
}

build() {
  cd "${srcdir}"

}

package() {
  source /etc/salome/profile.d/salome-kernel.sh

  cd "$srcdir/$_source"
  python2 setup.py install --prefix="${_installdir}" --root="${pkgdir}"
  
  mv "${srcdir}/V2014_2/tools/Salomemeca_pyutils_20142/lib/python2.7/site-packages"/* "${pkgdir}${_installdir}/lib/python2.7/site-packages/"
  
  install -D -m755 "$srcdir/$pkgname.profile" \
                   "$pkgdir/etc/salome/profile.d/$pkgname.sh"

}
md5sums=('171073103f5c91e55f61802071e3ca07'
         '8594f2096ceddb5b8485a2bdb096fbd8'
         '7e5cc6cf856d1f519b7f46accba1aefd')
