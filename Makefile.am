AUTOMAKE_OPTIONS = subdir-objects
#
# Exported from AX_PTHREAD:
pthread_CC	= @PTHREAD_CC@
pthread_CFLAGS	= @PTHREAD_CFLAGS@
pthread_LIBS	= @PTHREAD_LIBS@
have_PTHREAD	= @HAVE_PTHREAD@

# Exported from SSE2 library checks
have_SSE2_SIMD	    = @HAVE_SSE2_SIMD@
simd_SSE2_HEADER    = @SSE2_SIMD_HEADER@
# Also the use_SSE2_SIMD condition

# Exported from SSSE3 library checks
have_SSSE3_SIMD	    = @HAVE_SSSE3_SIMD@
simd_SSSE3_HEADER   = @SSSE3_SIMD_HEADER@
# Also the use_SSSE3_SIMD condition

# Return to your normal programming
#
AM_CC     = $(pthread_CC)
AM_LIBS   = $(pthrad_LIBS)
AM_CFLAGS = $(pthread_CFLAGS)

AM_CFLAGS += -I$(top_srcdir)/include
AM_CFLAGS += -I$(top_srcdir)/src
AM_CFLAGS += -I$(top_srcdir)/src/blake2

# From the --enable-listing feature option
if do_LISTING
AM_CFLAGS += -Wa,-adhlm=$(top_builddir)/$(@F).lst,--traditional-format  -g -fverbose-asm
endif

common_SRCS = src/argon2.c src/core.c src/blake2/blake2b.c src/thread.c src/encoding.c

if use_SSE2_SIMD
simd_SRC = src/opt.c
else
simd_SRC = src/ref.c
endif

bin_PROGRAMS = argon2 bench genkat

argon2_SOURCES = src/run.c $(common_SRCS) $(simd_SRC)
bench_SOURCES  = src/bench.c $(common_SRCS) $(simd_SRC)
genkat_SOURCES = src/genkat.c $(common_SRCS) $(simd_SRC)

# -Wa,-adhln=$(source).lst -g -fverbose-asm -masm=intel

