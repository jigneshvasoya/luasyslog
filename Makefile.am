rock=			$(PACKAGE_TARNAME)-$(PACKAGE_VERSION)-1.src.rock
rockspec=		$(PACKAGE_TARNAME)-$(PACKAGE_VERSION)-1.rockspec
c_sources=		lsyslog.c compat-5.3.c compat-5.3.h
lua_sources=		syslog.lua

EXTRA_DIST=		autogen.sh \
			README.md \
			COPYING \
			Makefile.am \
			test.lua.in \
			luasyslog.rockspec.in \
			$(c_sources) \
			$(lua_sources) \
			$(LMOD) \
			build/ax_define_subst.m4 \
			build/ax_lua.m4

TESTS=			test.lua
dist_pkgdata_DATA=	example.lua

ACLOCAL_AMFLAGS=	-I build
AM_CPPFLAGS=		-I. $(LUA_INCLUDE)
LIBADD=			$(LUA_LIB)


luaexec_LTLIBRARIES=	lsyslog.la
lsyslog_la_SOURCES=	$(c_sources)
lsyslog_la_LDFLAGS=	-module -avoid-version

loggingdir=		$(luadir)/logging
logging_DATA=		$(lua_sources)

CLEANFILES=		$(rock)


install-exec-hook:
	@$(POST_INSTALL)
	-rm -f $(DESTDIR)$(luaexecdir)/lsyslog.la

# The absence of the .la file prevents the .so removal
uninstall-hook:
	@$(POST_UNINSTALL)
	-rm -f $(DESTDIR)$(luaexecdir)/lsyslog.so

rock: $(rock)

$(rock): $(rockspec)
	$(AT_GEN)$(LUAROCKS) pack $<


.PHONY: rock
