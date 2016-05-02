#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.
AC_PREREQ([2.69])

# This project:
AC_INIT([argon2], [1.3], [https://github.com/janetizzy/phc-winner-argon2/issues],
		[argon2-1.3], [https://github.com/janetizzy/phc-winner-argon2])

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

# Check for the pthread library, a MUST HAVE for Argon2.
AX_PTHREAD(
    [AC_DEFINE(HAVE_PTHREAD, 1, [Define if you have POSIX threads libraries and header files.])
            AC_SUBST(PTHREAD_LIBS)
            AC_SUBST(PTHREAD_CFLAGS)
            AC_SUBST(PTHREAD_CC)
    ],
    [AC_MSG_FAILURE([Unable to find POSIX threads (libpthread) library.])]
    )
AC_SUBST(HAVE_PTHREAD)

## Development Options -

# Allow user to enable source/asm listing.
AC_ARG_ENABLE([listing], AS_HELP_STRING([--enable-listing], [Enable source/asm listing]))
AM_CONDITIONAL([do_LISTING], [test "x$enable_listing" == "xyes"])

# Allow user to enter a non-GCC name for Intel/AMD/GCC SSE2 intrinsics header.
AC_MSG_CHECKING([for user supplied SSE2 header])
AC_ARG_VAR(SSE2_SIMD_HEADER,
		  [Name of header that defines SSE2 intrinsics; default: emmintrin.h])

if test "x$SSE2_SIMD_HEADER" == "x"; then
	SSE2_SIMD_HEADER="emmintrin.h"
	AC_MSG_RESULT([standard header used.])
else
	AC_MSG_RESULT([alternate header used.])
fi

# Allow user to enter a non-GCC name for Intel/AMD/GCC SSSE3 intrinsics header.
AC_MSG_CHECKING([for user supplied SSSE3 header])
AC_ARG_VAR(SSSE3_SIMD_HEADER,
		  [Name of header that defines SSSE3 intrinsics; default: tmmintrin.h])

if test "x$SSSE3_SIMD_HEADER" == "x"; then
	SSSE3_SIMD_HEADER="tmmintrin.h"
	AC_MSG_RESULT([standard header used.])
else
	AC_MSG_RESULT([alternate header used.])
fi

# Check either the default or user specified SSE2 header for compile and link.
AC_MSG_NOTICE([checking the SSE2 header.])
sse2_save_cflags=$CFLAGS
CFLAGS="$CFLAGS -O0"
AC_LINK_IFELSE([AC_LANG_PROGRAM([#include <$SSE2_SIMD_HEADER>], [
__m128i av = {0ull, 0ull} ; __m128i bv = {0ull, 0ull} ; __m128i cv = {0ull, 0ull} ;
_mm_storeu_si128(&av, _mm_xor_si128(_mm_loadu_si128(&bv), _mm_loadu_si128(&cv))) ;])],
		[AC_SUBST(HAVE_SSE2_SIMD, 1)],
		[AC_SUBST(HAVE_SSE2_SIMD, 0)])
CFLAGS=$sse2_save_cflags
# Export the condition test to *.am
AM_CONDITIONAL([use_SSE2_SIMD], [test "$HAVE_SSE2_SIMD" == "1"])

# Check either the default or user specified SSSE3 header.
AC_MSG_NOTICE([checking the SSSE3 header.])
ssse3_save_cflags=$CFLAGS
CFLAGS="$CFLAGS -O0"
AC_LINK_IFELSE([AC_LANG_PROGRAM([#include <$SSSE3_SIMD_HEADER>], [
	__m128i mk = _mm_set_epi8(12, 13, 14, 15, 8, 9, 10, 11, 4, 5, 6, 7, 0, 1, 2, 3) ;
	__m128i av = {0ull, 0ull} ; __m128i bv = {0ull, 0ull} ; __m128i cv = {0ull, 0ull} ;
	_mm_store_si128(&av, _mm_shuffle_epi8(_mm_alignr_epi8(
		_mm_load_si128(&bv), _mm_load_si128(&cv), 6), mk) ;])],
				[AC_SUBST(HAVE_SSSE3_SIMD, 1)],
				[AC_SUBST(HAVE_SSSE3_SIMD, 0)])
CFLAGS=$ssse3_save_CFLAGS
# Export the condition test to *.am
AM_CONDITIONAL([use_SSSE3_SIMD], [test "$HAVE_SSSE3_SIMD" == "1"])

# Checks for libraries.

# Checks for header files.
AC_CHECK_HEADERS(
[inttypes.h limits.h stddef.h stdint.h stdio.h stdlib.h string.h time.h assert.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_SIZE_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
AC_TYPE_UINT8_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_CHECK_FUNCS([memset strtoul])

AC_OUTPUT
