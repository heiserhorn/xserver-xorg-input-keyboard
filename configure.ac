#  Copyright 2005 Adam Jackson.
#
#  Permission is hereby granted, free of charge, to any person obtaining a
#  copy of this software and associated documentation files (the "Software"),
#  to deal in the Software without restriction, including without limitation
#  on the rights to use, copy, modify, merge, publish, distribute, sub
#  license, and/or sell copies of the Software, and to permit persons to whom
#  the Software is furnished to do so, subject to the following conditions:
#
#  The above copyright notice and this permission notice (including the next
#  paragraph) shall be included in all copies or substantial portions of the
#  Software.
#
#  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#  FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT.  IN NO EVENT SHALL
#  ADAM JACKSON BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
#  IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
#  CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
#
# Process this file with autoconf to produce a configure script

AC_PREREQ(2.60)
AC_INIT([xf86-input-keyboard],
        1.4.0,
        [https://bugs.freedesktop.org/enter_bug.cgi?product=xorg],
        xf86-input-keyboard)
AC_CONFIG_SRCDIR([Makefile.am])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_AUX_DIR(.)

# Initialize X.Org macros
m4_ifndef([XORG_MACROS_VERSION],
          [m4_fatal([must install xorg-macros 1.4 or later before running autoconf/autogen])])
XORG_MACROS_VERSION(1.4)
XORG_DEFAULT_OPTIONS

AM_INIT_AUTOMAKE([foreign dist-bzip2])

AM_MAINTAINER_MODE

DRIVER_NAME=kbd
AC_SUBST([DRIVER_NAME])

# Checks for programs.
AC_DISABLE_STATIC
AC_PROG_LIBTOOL

case $host_os in
  linux*)
    IS_LINUX="yes"
    ;;

  freebsd* | kfreebsd-gnu* | netbsd* | openbsd*)
    IS_BSD="yes"
    ;;

  solaris*)
    IS_SOLARIS="yes"
    ;;

  gnu*)
    IS_HURD="yes"
    ;;

  *)
    AC_MSG_ERROR([Your operating system is not supported by the kbd driver.
                  Contact xorg@lists.freedesktop.org if you are interested in
                  porting it.])
    ;;
esac
AM_CONDITIONAL(LINUX, [test "x$IS_LINUX" = xyes])
AM_CONDITIONAL(BSD, [test "x$IS_BSD" = xyes])
AM_CONDITIONAL(SOLARIS, [test "x$IS_SOLARIS" = xyes])
AM_CONDITIONAL(HURD, [test "x$IS_HURD" = xyes])

AC_ARG_WITH(xorg-module-dir,
            AC_HELP_STRING([--with-xorg-module-dir=DIR],
                           [Default xorg module directory [[default=$libdir/xorg/modules]]]),
            [moduledir="$withval"],
            [moduledir="$libdir/xorg/modules"])
AC_SUBST(moduledir)

# Checks for pkg-config packages
PKG_CHECK_MODULES(XORG, [xorg-server >= 1.2.99.0] xproto inputproto)

# Checks for libraries.

AC_OUTPUT([Makefile src/Makefile man/Makefile])
