# Maintainer: Sergej Pupykin <pupykin.s@gmail.com>
# Contributor:Techlive Zheng <techlivezheng at gmail dot com>

pkgname=phpvirtualbox
pkgver=4.1_2
pkgrel=1
pkgdesc="PHP/AJAX web interface for VirtualBox 4.*"
arch=(any)
url="http://code.google.com/p/phpvirtualbox/"
license=('GPL')
depends=('php')
backup=("etc/webapps/phpvirtualbox/.htaccess" "etc/webapps/phpvirtualbox/config.php")
source=(http://phpvirtualbox.googlecode.com/files/${pkgname}-${pkgver/_/-}.zip)
md5sums=('0bb2afd8d81857693d1537f8c11fcf25')

build() {
  true
}

package() {
  cd ${srcdir}/${pkgname}-${pkgver/_/-}

  mkdir -p ${pkgdir}/etc/webapps/phpvirtualbox

  install -D -m644 config.php-example ${pkgdir}/etc/webapps/phpvirtualbox/config.php

#  sed -e "s/var \\\$username = 'vbox';/var \\\$username = '';/g" \
#      -e "s/var \\\$password = 'pass';/var \\\$password = '';/g" \
#      -e "s/#var \\\$noAuth = true;/var \\\$noAuth = true;/g" \
#      -i ${pkgdir}/etc/webapps/phpvirtualbox/config.php

  # Apache configuration
  cat > ${pkgdir}/etc/webapps/phpvirtualbox/apache.example.conf <<EOF
  Alias /phpvirtualbox "/usr/share/webapps/phpvirtualbox"
  <Directory "/usr/share/webapps/phpvirtualbox">
    Options FollowSymlinks
    AllowOverride All
    Order allow,deny
    Allow from all
  </Directory>
EOF

  #  Deny access by default
  echo "deny from all" >> ${pkgdir}/etc/webapps/phpvirtualbox/.htaccess

  find . -type f -exec install -D -m644 {,${pkgdir}/usr/share/webapps/${pkgname}/}{} \;

  ln -s /etc/webapps/phpvirtualbox/.htaccess  ${pkgdir}/usr/share/webapps/phpvirtualbox/.htaccess
  ln -s /etc/webapps/phpvirtualbox/config.php ${pkgdir}/usr/share/webapps/phpvirtualbox/config.php
}
