# CorePKG build script for sCore.
# Copyright 2011-2012, 2015-2016 David Egan Evans <sinuhe@gnu.org>
#
# This software is provided 'as-is', without any express or implied
# warranty. In no event will the authors be held liable for any damages
# arising from the use of this software.
#
# Permission is granted to anyone to use this software for any purpose,
# including commercial applications, and to alter it and redistribute it
# freely, subject to the following restrictions:
#
# 1. The origin of this software must not be misrepresented; you must
# not claim that you wrote the original software. If you use this
# software in a product, an acknowledgment in the product documentation
# would be appreciated but is not required.
#
# 2. Altered source versions must be plainly marked as such, and must 
# not be misrepresented as being the original software.
#
# 3. This notice may not be removed or altered from any source distribution.

DIST=sCore
PKG=corepkg
VERSION=3

if test ! -w .
then echo 'Cannot write to this directory!' 1>&2; exit 2
fi

if test ! -f core.info
then echo "The core.info file is not present." 1>&2; exit 3
fi

if test -d /tmp/$DIST-$PKG/
then rm -rf /tmp/$DIST-$PKG/
fi

rm -rf $PKG-$VERSION
tar xzf $PKG-$VERSION.tar.gz || exit 4
cd $PKG-$VERSION || exit 5

mkdir -pm 755 /tmp/sCore-$PKG/bin
mkdir -pm 755 /tmp/sCore-$PKG/usr/man/man8
mkdir -pm 755 /tmp/sCore-$PKG/usr/share/$PKG
cp man/corepkg.8 /tmp/sCore-$PKG/usr/man/man8/
gzip /tmp/sCore-$PKG/usr/man/man8/corepkg.8
cp src/corepkg /tmp/sCore-$PKG/bin/ && chmod a+x /tmp/sCore-$PKG/bin/*
cp COPYING /tmp/sCore-$PKG/usr/share/$PKG
gzip /tmp/sCore-$PKG/usr/share/$PKG/COPYING

cd ..
cp core.info /tmp/$DIST-$PKG/
chmod -R u+w,go+r-w,a-s /tmp/$DIST-$PKG*/
find /tmp/$DIST-$PKG*/ -type d -exec chmod ugo+x "{}" \;
if test $(id -u) -ne 0
then echo "$PKG has been installed to /tmp/$DIST-$PKG/" 1>&2
	echo "Before packaging: chown -R root: /tmp/$DIST-$PKG/" 1>&2
else chown -R root: /tmp/$DIST-$PKG/
	corepkg -c /tmp/$DIST-$PKG/ && rm -rf /tmp/$DIST-$PKG/
fi
rm -rf $PKG-$VERSION
