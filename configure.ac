dnl                                                      -*-Autoconf-*-
dnl Process this file with autoconf to generate configure.
dnl
dnl The AX_* macros are defined in files in the top-level m4
dnl directory.

#####################################################################
# Set up configuration system
#####################################################################

AC_INIT([gEDA/gaf], [1.5.2], [geda-bug@seul.org], [gEDA-gaf])
AC_PREREQ([2.60])

AC_CONFIG_SRCDIR([libgeda/src/libgeda.c])
AC_CONFIG_AUX_DIR([build-tools])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_HEADER([config.h])

AM_INIT_AUTOMAKE

AC_GNU_SOURCE # FIXME for some reason this is needed?

#####################################################################
# Do version number magic
#####################################################################

AX_GIT_VERSION([20090328])

# This is used for keeping the ChangeLog files up-to-date
AC_SUBST([CHANGELOG_BASE], [1.0-20070526])

#####################################################################
# Win32/MinGW support
#####################################################################

# FIXME complete this
AC_CANONICAL_HOST

#####################################################################
# Check for compiling & linking tools
#####################################################################

AC_PROG_CC
AC_PROG_CPP

AC_LIBTOOL_WIN32_DLL
AC_DISABLE_STATIC
AC_PROG_LIBTOOL

AM_PROG_CC_C_O
AX_GCC_FLAGS([-Wall])

AM_PROG_LEX
AX_PROG_AWK
AX_PROG_GROFF

#####################################################################
# Internationalisation
#####################################################################

AM_NLS
AM_GNU_GETTEXT
AM_GNU_GETTEXT_VERSION([0.16])
AX_DESKTOP_I18N

#####################################################################
# Check for libraries that use pkg-config
#####################################################################

PKG_PROG_PKG_CONFIG

PKG_CHECK_MODULES(GUILE, [guile-1.8], ,
  AC_MSG_ERROR([Guile 1.8 or later is required.]))

PKG_CHECK_MODULES(GLIB, [glib-2.0 >= 2.12.0], ,
  AC_MSG_ERROR([GLib 2.12.0 or later is required.]))

PKG_CHECK_MODULES(GTK, [gtk+-2.0 >= 2.10.0], ,
  AC_MSG_ERROR([GTK+ 2.10.0 or later is required.]))

PKG_CHECK_MODULES(GDK_PIXBUF, [gdk-pixbuf-2.0 >= 0.15.0], ,
  AC_MSG_ERROR([GDK_PIXBUF 0.15.0 or later is required.]))

PKG_CHECK_MODULES(CAIRO, [cairo >= 1.2.0], ,
  AC_MSG_ERROR([CAIRO 1.2.0 or later is required.]))

#####################################################################
# Header files & particular functions
#####################################################################

AC_HEADER_SYS_WAIT

# FIXME these checks are obsolete, because every plausible platform
# provides what they check for.
AC_HEADER_STDC
AC_HEADER_DIRENT

# FIXME these checks may be pointless for one of three reasons: every
# even vaguely sane libc implementation provides them; we don't use
# any of their functions in favour of GLib alternatives; or we don't
# provide an alternative, so the build will fail anyway.
AC_CHECK_HEADERS([stdlib.h string.h unistd.h])

# FIXME since we don't have a sensible alternative, if these headers
# are missing we should fail. Also need to remove HAVE_ERRNO_H tests
# in the C source code, since if we *don't* have it the build will
# fail anyway.
AC_CHECK_HEADERS([errno.h fcntl.h])

# Check for rint in math library. FIXME do we actually need to test
# this? Should we use lrint instead?
AC_CHECK_LIB([m], [lrint],
             AC_DEFINE([HAVE_LRINT], 1,
                       [If your math library has lrint in it, define this]))

AC_CHECK_FUNCS([chown getlogin])

# Check if the getopt header is present
AC_CHECK_HEADERS([getopt.h])
# Check for getopt_long
# On FreeBSD the 'gnugetopt' library is needed.
AC_SEARCH_LIBS([getopt_long], [gnugetopt],
               AC_DEFINE([HAVE_GETOPT_LONG], 1,
                         [Define to 1 if you have the `getopt_long' function.]))

# Check for misc features of awk
AX_AWK_FEATURES

#####################################################################
# Optional things
#####################################################################

# Assertions
AX_OPTION_ASSERT
# API documentation
AX_OPTION_DOXYGEN
# XDG desktop files
AX_OPTION_XDG_DATA
# KDE 3 desktop files
AX_OPTION_KDE3_DATA
# XDG database updates
AX_OPTION_XDG_DB
# libstroke support
AX_OPTION_STROKE

#####################################################################
# Tool-specific setup
#####################################################################

# Where should data files be installed/searched for?
AX_DATA_DIRS
# Where should PCB footprints be searched for?
AX_PCB_DIRS
# Set up libgeda with the correct ld version number
AX_LIBGEDA([36:0:0])

#####################################################################
# Generate output
#####################################################################

AC_CONFIG_FILES([Makefile
                 intl/Makefile

                 libgeda/Makefile
                 libgeda/libgeda.pc
                 libgeda/po/domain.mak
                 libgeda/po/Makefile.in
                 libgeda/data/Makefile
                 libgeda/docs/Makefile
                 libgeda/include/Makefile
                 libgeda/lib/Makefile
                 libgeda/scheme/Makefile
                 libgeda/share/Makefile
                 libgeda/src/Makefile

                 gschem/Makefile
                 gschem/po/Makefile.in
                 gschem/docs/Makefile
                 gschem/include/Makefile
                 gschem/scripts/Makefile
                 gschem/src/Makefile
                 gschem/examples/Makefile
                 gschem/lib/Makefile
                 gschem/lib/system-gschemrc
                 gschem/data/Makefile
                 gschem/bitmap/Makefile
                 gschem/tests/Makefile
                 gschem/scheme/Makefile

                 gattrib/Makefile
                 gattrib/po/Makefile.in
                 gattrib/design/Makefile
                 gattrib/docs/Makefile
                 gattrib/include/Makefile
                 gattrib/lib/Makefile
                 gattrib/lib/system-gattribrc
                 gattrib/src/Makefile
                 gattrib/data/Makefile

                 gsymcheck/docs/Makefile
                 gsymcheck/include/Makefile
                 gsymcheck/lib/Makefile
                 gsymcheck/lib/system-gsymcheckrc
                 gsymcheck/src/Makefile
                 gsymcheck/tests/Makefile
                 gsymcheck/Makefile

                 gnetlist/Makefile
                 gnetlist/src/Makefile
                 gnetlist/include/Makefile
                 gnetlist/scheme/Makefile
                 gnetlist/examples/Makefile
                 gnetlist/tests/Makefile
                 gnetlist/tests/hierarchy/Makefile
                 gnetlist/tests/hierarchy2/Makefile
                 gnetlist/tests/drc2/Makefile
                 gnetlist/tests/common/Makefile
                 gnetlist/docs/Makefile
                 gnetlist/docs/vams/Makefile
                 gnetlist/examples/vams/Makefile
                 gnetlist/examples/vams/vhdl/Makefile
                 gnetlist/examples/vams/vhdl/basic-vhdl/Makefile
                 gnetlist/examples/vams/vhdl/new-vhdl/Makefile
                 gnetlist/examples/switcap/Makefile
                 gnetlist/lib/Makefile
                 gnetlist/utils/Makefile
                 gnetlist/scripts/Makefile
                 gnetlist/scripts/annotate.sh
                 gnetlist/scripts/bom_xref.sh
                 gnetlist/scripts/bompp.sh
                 gnetlist/scripts/sw2asc
                 gnetlist/lib/system-gnetlistrc

                 utils/Makefile
                 utils/docs/Makefile
                 utils/examples/Makefile
                 utils/examples/gmk_sym/Makefile
                 utils/examples/gsch2pcb/Makefile
                 utils/examples/tragesym/Makefile
                 utils/gschlas/Makefile
                 utils/gxyrs/Makefile
                 utils/include/Makefile
                 utils/lib/Makefile
                 utils/lib/system-gschlasrc
                 utils/man/Makefile
                 utils/scripts/Makefile
                 utils/src/Makefile
                 utils/tests/Makefile
                 utils/tests/gxyrs/Makefile
                 utils/tests/gxyrs/inputs/Makefile
                 utils/tests/gxyrs/outputs/Makefile
                 utils/tests/refdes_renum/Makefile
                 utils/tests/refdes_renum/inputs/Makefile
                 utils/tests/refdes_renum/outputs/Makefile

                 symbols/Makefile
                 symbols/documentation/Makefile

                 docs/Makefile
                 docs/scripts/Makefile
                 docs/toplevel/Makefile
                 docs/toplevel/gedadocs.html
                 docs/wiki/Makefile
                 docs/wiki/_detail/Makefile
                 docs/wiki/_media/Makefile
                 docs/wiki/lib/Makefile
                 docs/wiki/lib/exe/Makefile
                 docs/wiki/lib/images/Makefile
                 docs/wiki/lib/images/fileicons/Makefile
                 docs/wiki/lib/images/interwiki/Makefile
                 docs/wiki/lib/images/smileys/Makefile
                 docs/wiki/lib/plugins/Makefile
                 docs/wiki/lib/plugins/definitionlist/Makefile
                 docs/wiki/lib/plugins/definitionlist/images/Makefile
                 docs/wiki/lib/plugins/note/Makefile
                 docs/wiki/lib/plugins/note/images/Makefile
                 docs/wiki/lib/tpl/Makefile
                 docs/wiki/lib/tpl/geda/Makefile
                 docs/wiki/lib/tpl/geda/images/Makefile

                 examples/Makefile
                 examples/RF_Amp/Makefile
                 examples/RF_Amp/model/Makefile
                 examples/RF_Amp/sym/Makefile
                 examples/TwoStageAmp/Makefile
                 examples/gTAG/Makefile
                 examples/lightning_detector/Makefile
])
AC_OUTPUT