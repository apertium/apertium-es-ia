AC_PREREQ(2.52)

m4_define([required_apertium_version], [3.0.0])

AC_INIT([apertium-es-ia], [0.0.1], [foo@bar.com])
AM_INIT_AUTOMAKE([apertium-es-ia], [0.0.1], no-define)
AC_PROG_LN_S
AC_PROG_AWK
AC_CONFIG_HEADER([config])

PKG_CHECK_MODULES(APERTIUM,   apertium >= required_apertium_version, [], [PKG_CHECK_MODULES(APERTIUM,   apertium-3.2 >= required_apertium_version)])

PKG_CHECK_MODULES(REGTEST, apertium-regtest >= 0.0.1, [],
                  [AC_MSG_WARN([Running tests requires apertium-regtest])])

AP_MKINCLUDE

AC_OUTPUT([Makefile])
