AUTOMAKE_OPTIONS = subdir-objects

# Exported from AX_PTHREAD:
pthread_CC	= @PTHREAD_CC@
pthread_CFLAGS	= @PTHREAD_CFLAGS@
pthread_LIBS	= @PTHREAD_LIBS@
have_PTHREAD	= @HAVE_PTHREAD@

# Exported from SIMD available check
have_SIMD	= @HAVE_SIMD@
simd_header	= @SIMD_HEADER@

# Return to your normal programming
#
AM_CC     = $(pthread_CC)
AM_LIBS   = $(pthrad_LIBS)
AM_CFLAGS = $(pthread_CFLAGS)

AM_CFLAGS += -I$(top_srcdir)/include
AM_CFLAGS += -I$(top_srcdir)/src
AM_CFLAGS += -I$(top_srcdir)/src/blake2

common_SRCS = src/argon2.c src/core.c src/blake2/blake2b.c src/thread.c src/encoding.c

if SIMD
simd_SRC = src/opt.c
else
simd_SRC = src/ref.c
endif

bin_PROGRAMS = argon2 bench genkat

argon2_SOURCES = src/run.c $(common_SRCS) $(simd_SRC)
bench_SOURCES  = src/bench.c $(common_SRCS) $(simd_SRC)
genkat_SOURCES = src/genkat.c $(common_SRCS) $(simd_SRC)
