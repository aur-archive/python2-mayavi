# Maintainer: Andrzej Giniewicz <gginiu@gmail.com>
pkgname=python2-mayavi
pkgver=4.2.0
_githubtag=a1e562a
pkgrel=1
pkgdesc="The Mayavi scientific data 3-dimensional visualizer"
arch=('i686' 'x86_64')
url="https://github.com/enthought/mayavi"
license=('BSD')
depends=('ipython2' 'vtk' 'python2-traitsui' 'python2-apptools'
         'python2-envisage' 'wxpython')
makedepends=('python2-distribute' 'python2-sphinx' 'gcc')
conflicts=('python-enthought-mayavi' 'python2-mayavi-git' 'python-ets-mayavi-svn')
options=(!emptydirs)

source=("https://github.com/enthought/mayavi/tarball/${pkgver}")
md5sums=('b46fb048176002738de64eed8d2b447a')

build() {
  cd "$srcdir/enthought-mayavi-${_githubtag}"

  python2 setup.py build

  cd docs

  make SPHINXBUILD=sphinx-build2 html
}

package() {
  cd "$srcdir/enthought-mayavi-${_githubtag}"

  python2 setup.py install --root="$pkgdir"/ --optimize=1

  cp -r docs/build/* "${pkgdir}/usr/lib/python2.7/site-packages"

  sed -i -e "s|#![ ]*/usr/bin/env python$|#!/usr/bin/env python2|" \
    $(find "${pkgdir}" -name '*.py')
  sed -i -e "s|#![ ]*/usr/bin/env python$|#!/usr/bin/env python2|" \
    "$pkgdir/usr/lib/python2.7/site-packages/mayavi/tests/csv_files/csv_2_py"

  install -D "LICENSE.txt" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

