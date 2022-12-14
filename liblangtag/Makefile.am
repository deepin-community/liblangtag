##
# Global definitions
NULL =
SUBDIRS =
AM_CPPFLAGS =							\
	-I$(top_srcdir)/liblangtag/				\
	-I$(top_srcdir)						\
	-I$(top_builddir)/liblangtag/				\
	-I$(top_builddir)					\
	-D__LANGTAG_COMPILATION					\
	-D__LANGTAG_PRIVATE					\
	-DBUILDDIR="\"$(abs_top_builddir)\""			\
	-DSRCDIR="\"$(abs_top_srcdir)\""			\
	-DREGDATADIR="\"$(datadir)/liblangtag\""		\
	-DLANGTAG_EXT_MODULE_PATH="\"$(LANGTAG_MODULEDIR)\""	\
	$(LIBXML2_CFLAGS)					\
	$(PTHREAD_CFLAGS)					\
	$(NULL)
LIBS =						\
	@LDFLAGS@				\
	$(LIBXML2_LIBS)				\
	$(PTHREAD_LIBS)				\
	$(NULL)
EXTRA_DIST =					\
	buildaliastbl.sh			\
	$(NULL)
MAINTAINERCLEANFILES =				\
	$(liblangtag_built_public_headers)	\
	$(liblangtag_built_private_headers)	\
	$(liblangtag_built_sources)		\
	$(stamp_files)				\
	$(NULL)
DISTCLEANFILES =				\
	stamp-lt-config				\
	stamp-lt-stdint				\
	lt-config.h				\
	lt-stdint.h				\
	$(NULL)
CLEANFILES =					\
	xgen-h					\
	xgen-c					\
	$(NULL)
BUILT_SOURCES =					\
	$(liblangtag_built_public_headers)	\
	$(liblangtag_built_private_headers)	\
	$(liblangtag_built_sources)		\
	stamp-lt-config				\
	stamp-lt-stdint				\
	$(NULL)

##
# Local definitions
liblangtag_public_headers =			\
	lt-database.h				\
	lt-error.h				\
	lt-ext-module.h				\
	lt-ext-module-data.h			\
	lt-extension.h				\
	lt-extlang.h				\
	lt-extlang-db.h				\
	lt-grandfathered.h			\
	lt-grandfathered-db.h			\
	lt-iter.h				\
	lt-lang.h				\
	lt-lang-db.h				\
	lt-list.h				\
	lt-macros.h				\
	lt-messages.h				\
	lt-redundant.h				\
	lt-redundant-db.h			\
	lt-region.h				\
	lt-region-db.h				\
	lt-relation-db.h			\
	lt-script.h				\
	lt-script-db.h				\
	lt-string.h				\
	lt-tag.h				\
	lt-utils.h				\
	lt-variant.h				\
	lt-variant-db.h				\
	lt-xml.h				\
	$(NULL)
liblangtag_private_headers =			\
	lt-atomic.h				\
	lt-ext-module-private.h			\
	lt-extension-private.h			\
	lt-extlang-private.h			\
	lt-grandfathered-private.h		\
	lt-iter-private.h			\
	lt-lang-private.h			\
	lt-lock.h				\
	lt-mem.h				\
	lt-redundant-private.h			\
	lt-region-private.h			\
	lt-script-private.h			\
	lt-stdint.h				\
	lt-tag-private.h			\
	lt-trie.h				\
	lt-variant-private.h			\
	$(NULL)
liblangtag_built_public_headers =		\
	lt-config.h				\
	$(NULL)
liblangtag_built_private_headers =		\
	lt-localealias.h			\
	$(NULL)
#
liblangtag_built_sources =			\
	$(NULL)
liblangtag_sources =				\
	$(liblangtag_built_sources)		\
	lt-database.c				\
	lt-error.c				\
	lt-ext-module.c				\
	lt-ext-module-data.c			\
	lt-extension.c				\
	lt-extlang.c				\
	lt-extlang-db.c				\
	lt-grandfathered.c			\
	lt-grandfathered-db.c			\
	lt-iter.c				\
	lt-lang.c				\
	lt-lang-db.c				\
	lt-list.c				\
	lt-mem.c				\
	lt-messages.c				\
	lt-redundant.c				\
	lt-redundant-db.c			\
	lt-region.c				\
	lt-region-db.c				\
	lt-relation-db.c			\
	lt-script.c				\
	lt-script-db.c				\
	lt-string.c				\
	lt-tag.c				\
	lt-trie.c				\
	lt-utils.c				\
	lt-variant.c				\
	lt-variant-db.c				\
	lt-xml.c				\
	$(NULL)
#
stamp_files =					\
	$(NULL)
included_modules = $(NULL)

if !ENABLE_MODULE
included_modules +=						\
	$(top_builddir)/extensions/liblangtag-ext-ldml-t.la	\
	$(top_builddir)/extensions/liblangtag-ext-ldml-u.la	\
	$(NULL)
endif

##
# Local Rules
lt-localealias.h: @BUILD_LOCALEALIAS@ Makefile
	$(AM_V_GEN) $(srcdir)/buildaliastbl.sh @LOCALE_ALIAS@ > $@.tmp && mv $@.tmp $@ || rm -f $@.tmp
	@if [ ! -f $(builddir)/$@ ]; then			\
		echo "Failed to generate $@.";			\
		exit 1;						\
	fi
stamp-lt-stdint: $(top_builddir)/config.status
	$(AM_V_GEN) cd $(top_builddir) &&			\
	$(SHELL) ./config.status liblangtag/lt-stdint.h
	@touch $@
	$(NULL)
stamp-lt-config: $(top_builddir)/config.status
	$(AM_V_GEN) cd $(top_builddir) &&			\
	$(SHELL) ./config.status liblangtag/lt-config.h
	@touch $@
	$(NULL)

if !ENABLE_MODULE
included-modules:
	$(AM_V_GEN) cd $(top_builddir)/extensions && $(MAKE) $(AM_MAKEFLAGS)
$(included_modules): included-modules
	$(AM_V_GEN) true

.PHONY: included-modules
endif

##
# Target platform
lib_LTLIBRARIES = 				\
	liblangtag.la				\
	$(NULL)
#
liblangtagincdir = $(includedir)/liblangtag
liblangtaginc_HEADERS =				\
	langtag.h				\
	$(liblangtag_public_headers)		\
	$(liblangtag_built_public_headers)	\
	$(NULL)
#
noinst_HEADERS =				\
	$(liblangtag_private_headers)		\
	$(liblangtag_built_private_headers)	\
	$(NULL)
#
liblangtag_la_SOURCES =			\
	$(liblangtag_sources)		\
	$(NULL)
liblangtag_la_CFLAGS =				\
	-DG_LOG_DOMAIN="\"LangTag\""		\
	$(NULL)
liblangtag_la_LIBADD =						\
	$(LIBS)							\
	$(included_modules)					\
	@MODULE_LIBS@ 							\
	$(NULL)
liblangtag_la_DEPENDENCIES =					\
	$(included_modules)					\
	$(NULL)
liblangtag_la_LDFLAGS =						\
	$(LDFLAGS)						\
	-version-info $(LT_CURRENT):$(LT_REVISION):$(LT_AGE)	\
	$(NULL)

-include $(top_srcdir)/git.mk
