AUTOMAKE_OPTIONS = subdir-objects

AM_CFLAGS  = -I$(top_srcdir)/include
AM_CFLAGS += -I$(top_srcdir)/src
AM_CFLAGS += -I$(top_srcdir)/src/blake2

bin_PROGRAMS = argon2 
argon2_SOURCES = \
	src/argon2.c src/core.c src/blake2/blake2b.c \
	src/thread.c src/encoding.c src/run.c src/opt.c
argon2_LDFLAGS = '-lpthread'
