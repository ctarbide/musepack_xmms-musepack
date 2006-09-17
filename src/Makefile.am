AUTOMAKE_OPTIONS = foreign

lib_LTLIBRARIES = libmpc.la

libdir = @XMMS_INPUT_PLUGIN_DIR@

INCLUDES = @GLIB_CFLAGS@ @XMMS_CFLAGS@ @GTK_CFLAGS@ @TAGLIB_CFLAGS@ -DVERSION=\"@VERSION@\"
libmpc_la_LIBADD = @PTHREAD_LIBS@ @GLIB_LIBS@ @XMMS_LIBS@ @GTK_LIBS@ @TAGLIB_LIBS@

libmpc_la_SOURCES = equalizer.cpp libmpc.cpp
libmpc_la_LDFLAGS = -lmpcdec -avoid-version
noinst_HEADERS = equalizer.h libmpc.h

