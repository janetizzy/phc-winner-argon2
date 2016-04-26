#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.
AC_PREREQ([2.69])

# This project:
AC_INIT([argon2], [1.3], [https://github.com/P-H-C/phc-winner-argon2/issues], [argon2-1.3])

# Add-in:
m4_include([m4/ax_pthread.m4])

# Organizational matters:
AC_CONFIG_SRCDIR([src/argon2.c])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES([Makefile])

# Be strict during developmnet:
AM_INIT_AUTOMAKE([subdir-objects -Wall -Werror])

# Checks for programs.
AC_PROG_INSTALL
AC_PROG_CC
AC_PROG_MAKE_SET

# Checks for libraries.
AX_PTHREAD( [
            AC_DEFINE(HAVE_PTHREAD,1,[Define if you have POSIX threads libraries and header files.])
            CLIBS="$PTHREAD_LIBS $LIBS"
            CFLAGS="$CFLAGS $PTHREAD_CFLAGS"
            LDFLAGS="$LDFLAGS $PTHREAD_CFLAGS"
            CC="$PTHREAD_CC"],
            [AC_MSG_FAILURE([Unable to find POSIX threads (libpthread) library.])])
            
# Checks for header files.
AC_CHECK_HEADERS([inttypes.h limits.h stddef.h stdint.h stdlib.h string.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_SIZE_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
AC_TYPE_UINT8_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_CHECK_FUNCS([memset strtoul])

AC_OUTPUT
