AC_INIT
AC_CONFIG_SRCDIR([src/libmpc.cpp])
AC_CONFIG_AUX_DIR(config)
AM_INIT_AUTOMAKE(libmpc,1.2.1)
AC_CONFIG_HEADER(src/config.h)

VERSION="1.2.1"

AC_PROG_CXX
AM_DISABLE_STATIC
AC_PROG_LIBTOOL
AC_PROG_INSTALL

CXXFLAGS="-O3 -fomit-frame-pointer"

AC_HEADER_STDC
AC_CHECK_HEADERS([fcntl.h stdlib.h string.h unistd.h wchar.h])

AC_HEADER_STDBOOL
AC_C_CONST
AC_TYPE_OFF_T
AC_TYPE_SIZE_T

AM_PATH_XMMS(1.2.10,,AC_MSG_ERROR([*** Xmms not installed - please install first ***]))

PKG_CHECK_MODULES(GTK, [gtk+ >= 1.2.2],
	[],
	[AC_MSG_ERROR([GTK+ >= 1.2.2 development package not installed])]
)

PKG_CHECK_MODULES(GLIB, [glib >= 1.2.10],
	[],
	[AC_MSG_ERROR([GLib+ >= 1.2.10 development package not installed])]
)

AC_CHECK_HEADERS(mpcdec/config_types.h,,AC_MSG_ERROR([*** Libmpcdec not installed - please install first ***]))

AC_DEFUN([AC_HAVE_TAGLIB],
[
    AC_DEFINE(HAVE_TAGLIB, 1, [Have TagLib])
    TAGLIB_CFLAGS=[`$TAGLIB_CONFIG --cflags`]
    TAGLIB_LIBS=[`$TAGLIB_CONFIG --libs`]
    HAVE_TAGLIB=true
])
AC_DEFUN([AC_NO_TAGLIB],
[
    AC_MSG_ERROR([*** Taglib not installed - please install first])
])

AC_PATH_PROG(TAGLIB_CONFIG, taglib-config, [no], [$PATH:$prefix/bin])
if test "x$TAGLIB_CONFIG" = "xno" ; then
    AC_NO_TAGLIB
else
    AC_HAVE_TAGLIB
fi
AC_SUBST(TAGLIB_CFLAGS)
AC_SUBST(TAGLIB_LIBS)

dnl ---------- END TAGLIB CHECK ----------

dnl pthread libs

AC_CHECK_HEADER(pthread.h,,AC_MSG_ERROR([*** POSIX thread support not installed - please install first ***]))

PTHREAD_LIBS=error
AC_MSG_CHECKING(for old style FreeBSD -pthread flag)
AC_EGREP_CPP(yes,
	[#if (defined(__FreeBSD_cc_version) && __FreeBSD_cc_version <= 500001) || defined(__OpenBSD__)
	  yes
	#endif
	], AC_MSG_RESULT(yes)
	CFLAGS="$CFLAGS -D_THREAD_SAFE" PTHREAD_LIBS="-pthread",
	AC_MSG_RESULT(no))
if test "x$PTHREAD_LIBS" = xerror; then
	AC_CHECK_LIB(pthread, pthread_attr_init,
		PTHREAD_LIBS="-lpthread")
fi
if test "x$PTHREAD_LIBS" = xerror; then
	AC_CHECK_LIB(pthreads, pthread_attr_init,
     		PTHREAD_LIBS="-lpthreads")
fi
if test "x$PTHREAD_LIBS" = xerror; then
	AC_CHECK_LIB(c_r, pthread_attr_init,
     		PTHREAD_LIBS="-lc_r")
fi
if test "x$PTHREAD_LIBS" = xerror; then
	AC_CHECK_FUNC(pthread_attr_init, PTHREAD_LIBS="")
fi
if test "x$PTHREAD_LIBS" = xerror; then
	AC_MSG_ERROR(*** Unable to locate working posix thread library ***)
fi
AC_SUBST(PTHREAD_LIBS)

dnl

AC_SUBST(VERSION)
AC_CONFIG_FILES([Makefile src/Makefile])
AC_OUTPUT
AC_MSG_RESULT([=> Xmms-musepack $VERSION configured successfully.])
