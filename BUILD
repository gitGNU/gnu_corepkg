# CorePKG build script for sGOS.
# Copyright 2011-2012, 2015 David Egan Evans <sinuhe@gnu.org>
#
# Permission to use, copy, modify, and distribute this software for
# any purpose with or without fee is hereby granted, provided that the
# above copyright notice and this permission notice appear in all
# copies.
#
# THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL
# WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED
# WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE
# AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL
# DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR
# PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER
# TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR
# PERFORMANCE OF THIS SOFTWARE.

PKG=corepkg
VERSION=2

if test ! -w .
then echo 'Cannot write to this directory!' 1>&2; exit 2
fi

if test -d /tmp/sGOS-$PKG/
then rm -rf /tmp/sGOS-$PKG || exit 3
fi

if test ! -f core.info
then echo "The core.info file is not present." 1>&2; exit 4
fi

rm -rf $PKG-$VERSION
tar xzvf $PKG-$VERSION.tar.gz
cd $PKG-$VERSION || exit 5

mkdir -pm 755 /tmp/sGOS-$PKG/bin
mkdir -pm 755 /tmp/sGOS-$PKG/usr/man/man8
mkdir -pm 755 /tmp/sGOS-$PKG/usr/share/$PKG
cp man/corepkg.8 /tmp/sGOS-$PKG/usr/man/man8/
cp src/corepkg /tmp/sGOS-$PKG/bin/ && chmod a+x /tmp/sGOS-$PKG/bin/*
cp COPYING /tmp/sGOS-$PKG/usr/share/$PKG

cd ..
cp core.info /tmp/sGOS-$PKG/ && chmod 0644 /tmp/sGOS-$PKG/core.info
chmod -R u+rw,go+r-w,ug-s /tmp/sGOS-$PKG
find /tmp/sGOS-$PKG -type d -exec chmod ugo+x "{}" \;
if test $(id -u) -ne 0
then echo "$PKG has been installed to /tmp/sGOS-$PKG/." 1>&2
	echo "It may be necessary to chown -R before packaging." 1>&2
else
	chown -R root: /tmp/sGOS-$PKG/
	corepkg -c /tmp/sGOS-$PKG/
fi
rm -rf $PKG-$VERSION
