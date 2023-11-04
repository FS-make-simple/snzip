# Command line tool.
snzip_SOURCES = src/snzip.c \
	src/snzip.h \
	src/snzip-format.c \
	src/framing-format.c \
	src/framing2-format.c \
	src/hadoop-snappy-format.c \
	src/iwa-format.c \
	src/snappy-java-format.c \
	src/snappy-in-java-format.c \
	src/comment-43-format.c \
	src/crc32.c \
	src/crc32.h
if SUPPORT_RAW_FORMAT
snzip_SOURCES += src/raw_format.cpp
endif
if HAVE_SSE4_2
snzip_SOURCES += src/crc32_sse4_2.c
endif
snzip_LDFLAGS = @LDFLAGS_SSE4_2@
CFLAGS_SSE4_2 = @CFLAGS_SSE4_2@
PROGS = snzip
bin_PROGRAMS = $(PROGS)

EXTRA_DIST = CMakeLists.txt cmake_config.h.in spec/snzip.spec win32/ya_getopt.c win32/ya_getopt.h
dist_doc_DATA = AUTHORS ChangeLog COPYING INSTALL NEWS README.md

dist-hook:
	git log > $(distdir)/ChangeLog

install-exec-hook:
	ln $(DESTDIR)$(bindir)/snzip$(EXEEXT) $(DESTDIR)$(bindir)/snunzip$(EXEEXT)
	ln $(DESTDIR)$(bindir)/snzip$(EXEEXT) $(DESTDIR)$(bindir)/snzcat$(EXEEXT)

uninstall-hook:
	rm -f $(DESTDIR)$(bindir)/snunzip$(EXEEXT)
	rm -f $(DESTDIR)$(bindir)/snzcat$(EXEEXT)

# Use CFLAGS_SSE4_2 only for crc32_sse4_2.c.
# Otherwise, SSE4.2 instructions may be used elsewhere.
src/crc32_sse4_2.o: src/crc32_sse4_2.c src/crc32.h
	$(COMPILE) $(CFLAGS_SSE4_2) -c $< -o $@
