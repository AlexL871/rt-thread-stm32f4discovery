#!/usr/make
#
# Makefile for SQLITE
#
# This makefile is suppose to be configured automatically using the
# autoconf.  But if that does not work for you, you can configure
# the makefile manually.  Just set the parameters below to values that
# work well for your system.
#
# If the configure script does not work out-of-the-box, you might
# be able to get it to work by giving it some hints.  See the comment
# at the beginning of configure.in for additional information.
#

# The toplevel directory of the source tree.  This is the directory
# that contains this "Makefile.in" and the "configure.in" script.
#
TOP = .

# C Compiler and options for use in building executables that
# will run on the platform that is doing the build.
#
BCC = gcc  -g -O2

# C Compile and options for use in building executables that 
# will run on the target platform.  (BCC and TCC are usually the
# same unless your are cross-compiling.)
#
TCC = gcc   -g -O2 -DSQLITE_OS_UNIX=1 -I. -I${TOP}/src -I${TOP}/ext/rtree

# Define this for the autoconf-based build, so that the code knows it can
# include the generated config.h
# 
TCC += -D_HAVE_SQLITE_CONFIG_H

# Define -DNDEBUG to compile without debugging (i.e., for production usage)
# Omitting the define will cause extra debugging code to be inserted and
# includes extra comments when "EXPLAIN stmt" is used.
#
TCC += -DNDEBUG 

# test UFFS
TCC += -DUFFS_TEST

UFFS_BUILD_PATH = $(HOME)/build/uffs

# Compiler options needed for programs that use the TCL library.
#
TCC += -I/usr/include/tcl8.5

# The library that programs using TCL must link against.
#
LIBTCL = -L/usr/lib -ltcl8.5 -ldl  -lpthread -lieee -lm

# Compiler options needed for programs that use the readline() library.
#
READLINE_FLAGS = -DHAVE_READLINE=1 -I/usr/include/readline

# The library that programs using readline() must link against.
#
LIBREADLINE = -lreadline -lreadline 

# Should the database engine be compiled threadsafe
#
TCC += -DSQLITE_THREADSAFE=1

# Any target libraries which libsqlite must be linked against
# 
TLIBS = -lpthread -L$(UFFS_BUILD_PATH)/src/test/api_test -lapitest_sqlite3


# Flags controlling use of the in memory btree implementation
#
# SQLITE_TEMP_STORE is 0 to force temporary tables to be in a file, 1 to
# default to file, 2 to default to memory, and 3 to force temporary
# tables to always be in memory.
#
TEMP_STORE = -DSQLITE_TEMP_STORE=1

# Enable/disable loadable extensions, and other optional features
# based on configuration. (-DSQLITE_OMIT*, -DSQLITE_ENABLE*).  
# The same set of OMIT and ENABLE flags should be passed to the 
# LEMON parser generator and the mkkeywordhash tool as well.
OPT_FEATURE_FLAGS = -DSQLITE_OMIT_LOAD_EXTENSION=1

TCC += $(OPT_FEATURE_FLAGS)

# Add in any optional parameters specified on the make commane line
# ie.  make "OPTS=-DSQLITE_ENABLE_FOO=1 -DSQLITE_OMIT_FOO=1".
TCC += $(OPTS)

# Version numbers and release number for the SQLite being compiled.
#
VERSION = 3.7
VERSION_NUMBER = 3007009
RELEASE = 3.7.9

# Filename extensions
#
BEXE = 
TEXE = 

# The following variable is "1" if the configure script was able to locate
# the tclConfig.sh file.  It is an empty string otherwise.  When this
# variable is "1", the TCL extension library (libtclsqlite3.so) is built
# and installed.
#
HAVE_TCL = 1

# This is the command to use for tclsh - normally just "tclsh", but we may
# know the specific version we want to use
#
TCLSH_CMD = tclsh8.5

# Where do we want to install the tcl plugin
#
TCLLIBDIR = /usr/share/tcltk/tcl8.5/sqlite3

# The suffix used on shared libraries.  Ex:  ".dll", ".so", ".dylib"
#
SHLIB_SUFFIX = @TCL_SHLIB_SUFFIX@

# If gcov support was enabled by the configure script, add the appropriate
# flags here.  It's not always as easy as just having the user add the right
# CFLAGS / LDFLAGS, because libtool wants to use CFLAGS when linking, which
# causes build errors with -fprofile-arcs -ftest-coverage with some GCCs.  
# Supposedly GCC does the right thing if you use --coverage, but in 
# practice it still fails.  See:
#
# http://www.mail-archive.com/debian-gcc@lists.debian.org/msg26197.html
#
# for more info.
#
GCOV_CFLAGS1 = -DSQLITE_COVERAGE_TEST=1 -fprofile-arcs -ftest-coverage
GCOV_LDFLAGS1 = -lgcov
USE_GCOV = 0
LTCOMPILE_EXTRAS += $(GCOV_CFLAGS$(USE_GCOV))
LTLINK_EXTRAS += $(GCOV_LDFLAGS$(USE_GCOV))


# The directory into which to store package information for

# Some standard variables and programs
#
prefix = /usr/local
exec_prefix = ${prefix}
libdir = ${exec_prefix}/lib
pkgconfigdir = $(libdir)/pkgconfig
bindir = ${exec_prefix}/bin
includedir = ${prefix}/include
INSTALL = /usr/bin/install -c
LIBTOOL = ./libtool
ALLOWRELEASE = 

# libtool compile/link/install
LTCOMPILE = $(LIBTOOL) --mode=compile --tag=CC $(TCC) $(LTCOMPILE_EXTRAS)
LTLINK = $(LIBTOOL) --mode=link $(TCC) $(LTCOMPILE_EXTRAS)  $(LTLINK_EXTRAS)
LTINSTALL = $(LIBTOOL) --mode=install $(INSTALL)

# nawk compatible awk.
NAWK = gawk

# You should not have to change anything below this line
###############################################################################

USE_AMALGAMATION = 1

# Object files for the SQLite library (non-amalgamation).
#
LIBOBJS0 = alter.lo analyze.lo attach.lo auth.lo \
         backup.lo bitvec.lo btmutex.lo btree.lo build.lo \
         callback.lo complete.lo ctime.lo date.lo delete.lo \
         expr.lo fault.lo fkey.lo \
         fts3.lo fts3_aux.lo fts3_expr.lo fts3_hash.lo fts3_icu.lo fts3_porter.lo \
         fts3_snippet.lo fts3_tokenizer.lo fts3_tokenizer1.lo fts3_write.lo \
         func.lo global.lo hash.lo \
         icu.lo insert.lo journal.lo legacy.lo loadext.lo \
         main.lo malloc.lo mem0.lo mem1.lo mem2.lo mem3.lo mem5.lo \
         memjournal.lo \
         mutex.lo mutex_noop.lo mutex_os2.lo mutex_unix.lo mutex_w32.lo \
         notify.lo opcodes.lo os.lo os_os2.lo os_unix.lo os_win.lo \
         pager.lo parse.lo pcache.lo pcache1.lo pragma.lo prepare.lo printf.lo \
         random.lo resolve.lo rowset.lo rtree.lo select.lo status.lo \
         table.lo tokenize.lo trigger.lo \
         update.lo util.lo vacuum.lo \
         vdbe.lo vdbeapi.lo vdbeaux.lo vdbeblob.lo vdbemem.lo vdbesort.lo \
         vdbetrace.lo wal.lo walker.lo where.lo utf.lo vtab.lo

# Object files for the amalgamation.
#
LIBOBJS1 = sqlite3.lo

# Determine the real value of LIBOBJ based on the 'configure' script
#
LIBOBJ = $(LIBOBJS$(USE_AMALGAMATION))


# All of the source code files.
#
SRC = \
  $(TOP)/src/alter.c \
  $(TOP)/src/analyze.c \
  $(TOP)/src/attach.c \
  $(TOP)/src/auth.c \
  $(TOP)/src/backup.c \
  $(TOP)/src/bitvec.c \
  $(TOP)/src/btmutex.c \
  $(TOP)/src/btree.c \
  $(TOP)/src/btree.h \
  $(TOP)/src/btreeInt.h \
  $(TOP)/src/build.c \
  $(TOP)/src/callback.c \
  $(TOP)/src/complete.c \
  $(TOP)/src/ctime.c \
  $(TOP)/src/date.c \
  $(TOP)/src/delete.c \
  $(TOP)/src/expr.c \
  $(TOP)/src/fault.c \
  $(TOP)/src/fkey.c \
  $(TOP)/src/func.c \
  $(TOP)/src/global.c \
  $(TOP)/src/hash.c \
  $(TOP)/src/hash.h \
  $(TOP)/src/hwtime.h \
  $(TOP)/src/insert.c \
  $(TOP)/src/journal.c \
  $(TOP)/src/legacy.c \
  $(TOP)/src/loadext.c \
  $(TOP)/src/main.c \
  $(TOP)/src/malloc.c \
  $(TOP)/src/mem0.c \
  $(TOP)/src/mem1.c \
  $(TOP)/src/mem2.c \
  $(TOP)/src/mem3.c \
  $(TOP)/src/mem5.c \
  $(TOP)/src/memjournal.c \
  $(TOP)/src/mutex.c \
  $(TOP)/src/mutex.h \
  $(TOP)/src/mutex_noop.c \
  $(TOP)/src/mutex_os2.c \
  $(TOP)/src/mutex_unix.c \
  $(TOP)/src/mutex_w32.c \
  $(TOP)/src/notify.c \
  $(TOP)/src/os.c \
  $(TOP)/src/os.h \
  $(TOP)/src/os_common.h \
  $(TOP)/src/os_os2.c \
  $(TOP)/src/os_unix.c \
  $(TOP)/src/os_win.c \
  $(TOP)/src/pager.c \
  $(TOP)/src/pager.h \
  $(TOP)/src/parse.y \
  $(TOP)/src/pcache.c \
  $(TOP)/src/pcache.h \
  $(TOP)/src/pcache1.c \
  $(TOP)/src/pragma.c \
  $(TOP)/src/prepare.c \
  $(TOP)/src/printf.c \
  $(TOP)/src/random.c \
  $(TOP)/src/resolve.c \
  $(TOP)/src/rowset.c \
  $(TOP)/src/select.c \
  $(TOP)/src/status.c \
  $(TOP)/src/shell.c \
  $(TOP)/src/sqlite.h.in \
  $(TOP)/src/sqlite3ext.h \
  $(TOP)/src/sqliteInt.h \
  $(TOP)/src/sqliteLimit.h \
  $(TOP)/src/table.c \
  $(TOP)/src/tclsqlite.c \
  $(TOP)/src/tokenize.c \
  $(TOP)/src/trigger.c \
  $(TOP)/src/utf.c \
  $(TOP)/src/update.c \
  $(TOP)/src/util.c \
  $(TOP)/src/vacuum.c \
  $(TOP)/src/vdbe.c \
  $(TOP)/src/vdbe.h \
  $(TOP)/src/vdbeapi.c \
  $(TOP)/src/vdbeaux.c \
  $(TOP)/src/vdbeblob.c \
  $(TOP)/src/vdbemem.c \
  $(TOP)/src/vdbesort.c \
  $(TOP)/src/vdbetrace.c \
  $(TOP)/src/vdbeInt.h \
  $(TOP)/src/vtab.c \
  $(TOP)/src/wal.c \
  $(TOP)/src/wal.h \
  $(TOP)/src/walker.c \
  $(TOP)/src/where.c

# Source code for extensions
#
SRC += \
  $(TOP)/ext/fts1/fts1.c \
  $(TOP)/ext/fts1/fts1.h \
  $(TOP)/ext/fts1/fts1_hash.c \
  $(TOP)/ext/fts1/fts1_hash.h \
  $(TOP)/ext/fts1/fts1_porter.c \
  $(TOP)/ext/fts1/fts1_tokenizer.h \
  $(TOP)/ext/fts1/fts1_tokenizer1.c
SRC += \
  $(TOP)/ext/fts2/fts2.c \
  $(TOP)/ext/fts2/fts2.h \
  $(TOP)/ext/fts2/fts2_hash.c \
  $(TOP)/ext/fts2/fts2_hash.h \
  $(TOP)/ext/fts2/fts2_icu.c \
  $(TOP)/ext/fts2/fts2_porter.c \
  $(TOP)/ext/fts2/fts2_tokenizer.h \
  $(TOP)/ext/fts2/fts2_tokenizer.c \
  $(TOP)/ext/fts2/fts2_tokenizer1.c
SRC += \
  $(TOP)/ext/fts3/fts3.c \
  $(TOP)/ext/fts3/fts3.h \
  $(TOP)/ext/fts3/fts3Int.h \
  $(TOP)/ext/fts3/fts3_aux.c \
  $(TOP)/ext/fts3/fts3_expr.c \
  $(TOP)/ext/fts3/fts3_hash.c \
  $(TOP)/ext/fts3/fts3_hash.h \
  $(TOP)/ext/fts3/fts3_icu.c \
  $(TOP)/ext/fts3/fts3_porter.c \
  $(TOP)/ext/fts3/fts3_snippet.c \
  $(TOP)/ext/fts3/fts3_tokenizer.h \
  $(TOP)/ext/fts3/fts3_tokenizer.c \
  $(TOP)/ext/fts3/fts3_tokenizer1.c \
  $(TOP)/ext/fts3/fts3_write.c
SRC += \
  $(TOP)/ext/icu/sqliteicu.h \
  $(TOP)/ext/icu/icu.c
SRC += \
  $(TOP)/ext/rtree/rtree.h \
  $(TOP)/ext/rtree/rtree.c


# Generated source code files
#
SRC += \
  keywordhash.h \
  opcodes.c \
  opcodes.h \
  parse.c \
  parse.h \
  config.h \
  sqlite3.h

# Source code to the test files.
#
TESTSRC = \
  $(TOP)/src/test1.c \
  $(TOP)/src/test2.c \
  $(TOP)/src/test3.c \
  $(TOP)/src/test4.c \
  $(TOP)/src/test5.c \
  $(TOP)/src/test6.c \
  $(TOP)/src/test7.c \
  $(TOP)/src/test8.c \
  $(TOP)/src/test9.c \
  $(TOP)/src/test_autoext.c \
  $(TOP)/src/test_async.c \
  $(TOP)/src/test_backup.c \
  $(TOP)/src/test_btree.c \
  $(TOP)/src/test_config.c \
  $(TOP)/src/test_demovfs.c \
  $(TOP)/src/test_devsym.c \
  $(TOP)/src/test_func.c \
  $(TOP)/src/test_fuzzer.c \
  $(TOP)/src/test_hexio.c \
  $(TOP)/src/test_init.c \
  $(TOP)/src/test_intarray.c \
  $(TOP)/src/test_journal.c \
  $(TOP)/src/test_malloc.c \
  $(TOP)/src/test_multiplex.c \
  $(TOP)/src/test_mutex.c \
  $(TOP)/src/test_onefile.c \
  $(TOP)/src/test_osinst.c \
  $(TOP)/src/test_pcache.c \
  $(TOP)/src/test_quota.c \
  $(TOP)/src/test_rtree.c \
  $(TOP)/src/test_schema.c \
  $(TOP)/src/test_server.c \
  $(TOP)/src/test_superlock.c \
  $(TOP)/src/test_syscall.c \
  $(TOP)/src/test_stat.c \
  $(TOP)/src/test_tclvar.c \
  $(TOP)/src/test_thread.c \
  $(TOP)/src/test_vfs.c \
  $(TOP)/src/test_wholenumber.c \
  $(TOP)/src/test_wsd.c       \
  $(TOP)/ext/fts3/fts3_term.c \
  $(TOP)/ext/fts3/fts3_test.c 

# Source code to the library files needed by the test fixture
#
TESTSRC2 = \
  $(TOP)/src/attach.c \
  $(TOP)/src/backup.c \
  $(TOP)/src/bitvec.c \
  $(TOP)/src/btree.c \
  $(TOP)/src/build.c \
  $(TOP)/src/ctime.c \
  $(TOP)/src/date.c \
  $(TOP)/src/expr.c \
  $(TOP)/src/func.c \
  $(TOP)/src/insert.c \
  $(TOP)/src/wal.c \
  $(TOP)/src/mem5.c \
  $(TOP)/src/os.c \
  $(TOP)/src/os_os2.c \
  $(TOP)/src/os_unix.c \
  $(TOP)/src/os_win.c \
  $(TOP)/src/pager.c \
  $(TOP)/src/pragma.c \
  $(TOP)/src/prepare.c \
  $(TOP)/src/printf.c \
  $(TOP)/src/random.c \
  $(TOP)/src/pcache.c \
  $(TOP)/src/pcache1.c \
  $(TOP)/src/select.c \
  $(TOP)/src/tokenize.c \
  $(TOP)/src/utf.c \
  $(TOP)/src/util.c \
  $(TOP)/src/vdbeapi.c \
  $(TOP)/src/vdbeaux.c \
  $(TOP)/src/vdbe.c \
  $(TOP)/src/vdbemem.c \
  $(TOP)/src/vdbetrace.c \
  $(TOP)/src/where.c \
  parse.c \
  $(TOP)/ext/fts3/fts3.c \
  $(TOP)/ext/fts3/fts3_aux.c \
  $(TOP)/ext/fts3/fts3_expr.c \
  $(TOP)/ext/fts3/fts3_term.c \
  $(TOP)/ext/fts3/fts3_tokenizer.c \
  $(TOP)/ext/fts3/fts3_write.c \
  $(TOP)/ext/async/sqlite3async.c

# Header files used by all library source files.
#
HDR = \
   $(TOP)/src/btree.h \
   $(TOP)/src/btreeInt.h \
   $(TOP)/src/hash.h \
   $(TOP)/src/hwtime.h \
   keywordhash.h \
   $(TOP)/src/mutex.h \
   opcodes.h \
   $(TOP)/src/os.h \
   $(TOP)/src/os_common.h \
   $(TOP)/src/pager.h \
   $(TOP)/src/pcache.h \
   parse.h  \
   sqlite3.h  \
   $(TOP)/src/sqlite3ext.h \
   $(TOP)/src/sqliteInt.h  \
   $(TOP)/src/sqliteLimit.h \
   $(TOP)/src/vdbe.h \
   $(TOP)/src/vdbeInt.h \
   config.h

# Header files used by extensions
#
EXTHDR += \
  $(TOP)/ext/fts1/fts1.h \
  $(TOP)/ext/fts1/fts1_hash.h \
  $(TOP)/ext/fts1/fts1_tokenizer.h
EXTHDR += \
  $(TOP)/ext/fts2/fts2.h \
  $(TOP)/ext/fts2/fts2_hash.h \
  $(TOP)/ext/fts2/fts2_tokenizer.h
EXTHDR += \
  $(TOP)/ext/fts3/fts3.h \
  $(TOP)/ext/fts3/fts3Int.h \
  $(TOP)/ext/fts3/fts3_hash.h \
  $(TOP)/ext/fts3/fts3_tokenizer.h
EXTHDR += \
  $(TOP)/ext/rtree/rtree.h
EXTHDR += \
  $(TOP)/ext/icu/sqliteicu.h
EXTHDR += \
  $(TOP)/ext/rtree/sqlite3rtree.h

# This is the default Makefile target.  The objects listed here
# are what get build when you type just "make" with no arguments.
#
all:	sqlite3.h libsqlite3.la sqlite3$(TEXE) $(HAVE_TCL:1=libtclsqlite3.la)

Makefile: $(TOP)/Makefile.in
	./config.status

sqlite3.pc: $(TOP)/sqlite3.pc.in
	./config.status

libsqlite3.la:	$(LIBOBJ)
	$(LTLINK) -o $@ $(LIBOBJ) $(TLIBS) \
		${ALLOWRELEASE} -rpath "$(libdir)" -version-info "8:6:8"

libtclsqlite3.la:	tclsqlite.lo libsqlite3.la
	$(LTLINK) -o $@ tclsqlite.lo \
		libsqlite3.la -L/usr/lib -ltclstub8.5 $(TLIBS) \
		-rpath "$(TCLLIBDIR)" \
		-version-info "8:6:8" \
		-avoid-version

sqlite3$(TEXE):	$(TOP)/src/shell.c libsqlite3.la sqlite3.h
	$(LTLINK) $(READLINE_FLAGS) \
		-o $@ $(TOP)/src/shell.c libsqlite3.la \
		$(LIBREADLINE) $(TLIBS) -rpath "$(libdir)"

# This target creates a directory named "tsrc" and fills it with
# copies of all of the C source code and header files needed to
# build on the target system.  Some of the C source code and header
# files are automatically generated.  This target takes care of
# all that automatic generation.
#
.target_source:	$(SRC) $(TOP)/tool/vdbe-compress.tcl
	rm -rf tsrc
	mkdir tsrc
	cp -f $(SRC) tsrc
	rm tsrc/sqlite.h.in tsrc/parse.y
	$(TCLSH_CMD) $(TOP)/tool/vdbe-compress.tcl <tsrc/vdbe.c >vdbe.new
	mv vdbe.new tsrc/vdbe.c
	touch .target_source

sqlite3.c:	.target_source $(TOP)/tool/mksqlite3c.tcl
	$(TCLSH_CMD) $(TOP)/tool/mksqlite3c.tcl

sqlite3-all.c:	sqlite3.c $(TOP)/tool/split-sqlite3c.tcl
	$(TCLSH_CMD) $(TOP)/tool/split-sqlite3c.tcl

# Rule to build the amalgamation
#
sqlite3.lo:	sqlite3.c
	$(LTCOMPILE) $(TEMP_STORE) -c sqlite3.c

# Rules to build the LEMON compiler generator
#
lemon$(BEXE):	$(TOP)/tool/lemon.c $(TOP)/src/lempar.c
	$(BCC) -o $@ $(TOP)/tool/lemon.c
	cp $(TOP)/src/lempar.c .

# Rules to build individual *.o files from generated *.c files. This
# applies to:
#
#     parse.o
#     opcodes.o
#
parse.lo:	parse.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c parse.c

opcodes.lo:	opcodes.c
	$(LTCOMPILE) $(TEMP_STORE) -c opcodes.c

# Rules to build individual *.o files from files in the src directory.
#
alter.lo:	$(TOP)/src/alter.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/alter.c

analyze.lo:	$(TOP)/src/analyze.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/analyze.c

attach.lo:	$(TOP)/src/attach.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/attach.c

auth.lo:	$(TOP)/src/auth.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/auth.c

backup.lo:	$(TOP)/src/backup.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/backup.c

bitvec.lo:	$(TOP)/src/bitvec.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/bitvec.c

btmutex.lo:	$(TOP)/src/btmutex.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/btmutex.c

btree.lo:	$(TOP)/src/btree.c $(HDR) $(TOP)/src/pager.h
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/btree.c

build.lo:	$(TOP)/src/build.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/build.c

callback.lo:	$(TOP)/src/callback.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/callback.c

complete.lo:	$(TOP)/src/complete.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/complete.c

ctime.lo:	$(TOP)/src/ctime.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/ctime.c

date.lo:	$(TOP)/src/date.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/date.c

delete.lo:	$(TOP)/src/delete.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/delete.c

expr.lo:	$(TOP)/src/expr.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/expr.c

fault.lo:	$(TOP)/src/fault.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/fault.c

fkey.lo:	$(TOP)/src/fkey.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/fkey.c

func.lo:	$(TOP)/src/func.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/func.c

global.lo:	$(TOP)/src/global.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/global.c

hash.lo:	$(TOP)/src/hash.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/hash.c

insert.lo:	$(TOP)/src/insert.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/insert.c

journal.lo:	$(TOP)/src/journal.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/journal.c

legacy.lo:	$(TOP)/src/legacy.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/legacy.c

loadext.lo:	$(TOP)/src/loadext.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/loadext.c

main.lo:	$(TOP)/src/main.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/main.c

malloc.lo:	$(TOP)/src/malloc.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/malloc.c

mem0.lo:	$(TOP)/src/mem0.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/mem0.c

mem1.lo:	$(TOP)/src/mem1.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/mem1.c

mem2.lo:	$(TOP)/src/mem2.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/mem2.c

mem3.lo:	$(TOP)/src/mem3.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/mem3.c

mem5.lo:	$(TOP)/src/mem5.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/mem5.c

memjournal.lo:	$(TOP)/src/memjournal.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/memjournal.c

mutex.lo:	$(TOP)/src/mutex.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/mutex.c

mutex_noop.lo:	$(TOP)/src/mutex_noop.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/mutex_noop.c

mutex_os2.lo:	$(TOP)/src/mutex_os2.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/mutex_os2.c

mutex_unix.lo:	$(TOP)/src/mutex_unix.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/mutex_unix.c

mutex_w32.lo:	$(TOP)/src/mutex_w32.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/mutex_w32.c

notify.lo:	$(TOP)/src/notify.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/notify.c

pager.lo:	$(TOP)/src/pager.c $(HDR) $(TOP)/src/pager.h
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/pager.c

pcache.lo:	$(TOP)/src/pcache.c $(HDR) $(TOP)/src/pcache.h
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/pcache.c

pcache1.lo:	$(TOP)/src/pcache1.c $(HDR) $(TOP)/src/pcache.h
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/pcache1.c

os.lo:	$(TOP)/src/os.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/os.c

os_unix.lo:	$(TOP)/src/os_unix.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/os_unix.c

os_win.lo:	$(TOP)/src/os_win.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/os_win.c

os_os2.lo:	$(TOP)/src/os_os2.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/os_os2.c

pragma.lo:	$(TOP)/src/pragma.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/pragma.c

prepare.lo:	$(TOP)/src/prepare.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/prepare.c

printf.lo:	$(TOP)/src/printf.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/printf.c

random.lo:	$(TOP)/src/random.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/random.c

resolve.lo:	$(TOP)/src/resolve.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/resolve.c

rowset.lo:	$(TOP)/src/rowset.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/rowset.c

select.lo:	$(TOP)/src/select.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/select.c

status.lo:	$(TOP)/src/status.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/status.c

table.lo:	$(TOP)/src/table.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/table.c

tokenize.lo:	$(TOP)/src/tokenize.c keywordhash.h $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/tokenize.c

trigger.lo:	$(TOP)/src/trigger.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/trigger.c

update.lo:	$(TOP)/src/update.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/update.c

utf.lo:	$(TOP)/src/utf.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/utf.c

util.lo:	$(TOP)/src/util.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/util.c

vacuum.lo:	$(TOP)/src/vacuum.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/vacuum.c

vdbe.lo:	$(TOP)/src/vdbe.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/vdbe.c

vdbeapi.lo:	$(TOP)/src/vdbeapi.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/vdbeapi.c

vdbeaux.lo:	$(TOP)/src/vdbeaux.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/vdbeaux.c

vdbeblob.lo:	$(TOP)/src/vdbeblob.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/vdbeblob.c

vdbemem.lo:	$(TOP)/src/vdbemem.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/vdbemem.c

vdbesort.lo:	$(TOP)/src/vdbesort.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/vdbesort.c

vdbetrace.lo:	$(TOP)/src/vdbetrace.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/vdbetrace.c

vtab.lo:	$(TOP)/src/vtab.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/vtab.c

wal.lo:	$(TOP)/src/wal.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/wal.c

walker.lo:	$(TOP)/src/walker.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/walker.c

where.lo:	$(TOP)/src/where.c $(HDR)
	$(LTCOMPILE) $(TEMP_STORE) -c $(TOP)/src/where.c

tclsqlite.lo:	$(TOP)/src/tclsqlite.c $(HDR)
	$(LTCOMPILE) -DUSE_TCL_STUBS=1 -c $(TOP)/src/tclsqlite.c

tclsqlite-shell.lo:	$(TOP)/src/tclsqlite.c $(HDR)
	$(LTCOMPILE) -DTCLSH=1 -o $@ -c $(TOP)/src/tclsqlite.c

tclsqlite-stubs.lo:	$(TOP)/src/tclsqlite.c $(HDR)
	$(LTCOMPILE) -DUSE_TCL_STUBS=1 -o $@ -c $(TOP)/src/tclsqlite.c

tclsqlite3$(TEXE):	tclsqlite-shell.lo libsqlite3.la
	$(LTLINK) -o $@ tclsqlite-shell.lo \
		 libsqlite3.la $(LIBTCL)

# Rules to build opcodes.c and opcodes.h
#
opcodes.c:	opcodes.h $(TOP)/mkopcodec.awk
	$(NAWK) -f $(TOP)/mkopcodec.awk opcodes.h >opcodes.c

opcodes.h:	parse.h $(TOP)/src/vdbe.c $(TOP)/mkopcodeh.awk
	cat parse.h $(TOP)/src/vdbe.c | $(NAWK) -f $(TOP)/mkopcodeh.awk >opcodes.h

# Rules to build parse.c and parse.h - the outputs of lemon.
#
parse.h:	parse.c

parse.c:	$(TOP)/src/parse.y lemon$(BEXE) $(TOP)/addopcodes.awk
	cp $(TOP)/src/parse.y .
	rm -f parse.h
	./lemon$(BEXE) $(OPT_FEATURE_FLAGS) $(OPTS) parse.y
	mv parse.h parse.h.temp
	$(NAWK) -f $(TOP)/addopcodes.awk parse.h.temp >parse.h

sqlite3.h:	$(TOP)/src/sqlite.h.in $(TOP)/manifest.uuid $(TOP)/VERSION
	$(TCLSH_CMD) $(TOP)/tool/mksqlite3h.tcl $(TOP) >sqlite3.h

keywordhash.h:	$(TOP)/tool/mkkeywordhash.c
	$(BCC) -o mkkeywordhash$(BEXE) $(OPT_FEATURE_FLAGS) $(OPTS) $(TOP)/tool/mkkeywordhash.c
	./mkkeywordhash$(BEXE) >keywordhash.h



# Rules to build the extension objects.
#
icu.lo:	$(TOP)/ext/icu/icu.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/icu/icu.c

fts2.lo:	$(TOP)/ext/fts2/fts2.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts2/fts2.c

fts2_hash.lo:	$(TOP)/ext/fts2/fts2_hash.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts2/fts2_hash.c

fts2_icu.lo:	$(TOP)/ext/fts2/fts2_icu.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts2/fts2_icu.c

fts2_porter.lo:	$(TOP)/ext/fts2/fts2_porter.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts2/fts2_porter.c

fts2_tokenizer.lo:	$(TOP)/ext/fts2/fts2_tokenizer.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts2/fts2_tokenizer.c

fts2_tokenizer1.lo:	$(TOP)/ext/fts2/fts2_tokenizer1.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts2/fts2_tokenizer1.c

fts3.lo:	$(TOP)/ext/fts3/fts3.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts3/fts3.c

fts3_aux.lo:	$(TOP)/ext/fts3/fts3_aux.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts3/fts3_aux.c

fts3_expr.lo:	$(TOP)/ext/fts3/fts3_expr.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts3/fts3_expr.c

fts3_hash.lo:	$(TOP)/ext/fts3/fts3_hash.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts3/fts3_hash.c

fts3_icu.lo:	$(TOP)/ext/fts3/fts3_icu.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts3/fts3_icu.c

fts3_porter.lo:	$(TOP)/ext/fts3/fts3_porter.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts3/fts3_porter.c

fts3_snippet.lo:	$(TOP)/ext/fts3/fts3_snippet.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts3/fts3_snippet.c

fts3_tokenizer.lo:	$(TOP)/ext/fts3/fts3_tokenizer.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts3/fts3_tokenizer.c

fts3_tokenizer1.lo:	$(TOP)/ext/fts3/fts3_tokenizer1.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts3/fts3_tokenizer1.c

fts3_write.lo:	$(TOP)/ext/fts3/fts3_write.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/fts3/fts3_write.c

rtree.lo:	$(TOP)/ext/rtree/rtree.c $(HDR) $(EXTHDR)
	$(LTCOMPILE) -DSQLITE_CORE -c $(TOP)/ext/rtree/rtree.c


# Rules to build the 'testfixture' application.
#
# If using the amalgamation, use sqlite3.c directly to build the test
# fixture.  Otherwise link against libsqlite3.la.  (This distinction is
# necessary because the test fixture requires non-API symbols which are
# hidden when the library is built via the amalgamation).
#
TESTFIXTURE_FLAGS  = -DTCLSH=1 -DSQLITE_TEST=1 -DSQLITE_CRASH_TEST=1
TESTFIXTURE_FLAGS += -DSQLITE_SERVER=1 -DSQLITE_PRIVATE="" -DSQLITE_CORE 
TESTFIXTURE_FLAGS += -DBUILD_sqlite

TESTFIXTURE_SRC0 = $(TESTSRC2) libsqlite3.la
TESTFIXTURE_SRC1 = sqlite3.c
TESTFIXTURE_SRC = $(TESTSRC) $(TOP)/src/tclsqlite.c $(TESTFIXTURE_SRC$(USE_AMALGAMATION))

testfixture$(TEXE):	$(TESTFIXTURE_SRC)
	$(LTLINK) -DSQLITE_NO_SYNC=1 $(TEMP_STORE) $(TESTFIXTURE_FLAGS) \
		-o $@ $(TESTFIXTURE_SRC) $(LIBTCL) $(TLIBS)


fulltest:	testfixture$(TEXE) sqlite3$(TEXE)
	./testfixture$(TEXE) $(TOP)/test/all.test

soaktest:	testfixture$(TEXE) sqlite3$(TEXE)
	./testfixture$(TEXE) $(TOP)/test/all.test -soak=1

test:	testfixture$(TEXE) sqlite3$(TEXE)
	./testfixture$(TEXE) $(TOP)/test/veryquick.test

sqlite3_analyzer.c: sqlite3.c $(TOP)/src/test_stat.c $(TOP)/src/tclsqlite.c $(TOP)/tool/spaceanal.tcl
	echo "#define TCLSH 2" > $@
	cat sqlite3.c $(TOP)/src/test_stat.c $(TOP)/src/tclsqlite.c >> $@
	echo "static const char *tclsh_main_loop(void){" >> $@
	echo "static const char *zMainloop = " >> $@
	$(NAWK) -f $(TOP)/tool/tostr.awk $(TOP)/tool/spaceanal.tcl >> $@
	echo "; return zMainloop; }" >> $@

sqlite3_analyzer$(TEXE): sqlite3_analyzer.c
	$(LTLINK) sqlite3_analyzer.c -o $@ $(LIBTCL) $(TLIBS)

# Standard install and cleanup targets
#
lib_install:	libsqlite3.la
	$(INSTALL) -d $(DESTDIR)$(libdir)
	$(LTINSTALL) libsqlite3.la $(DESTDIR)$(libdir)
	
install:	sqlite3$(BEXE) lib_install sqlite3.h sqlite3.pc ${HAVE_TCL:1=tcl_install}
	$(INSTALL) -d $(DESTDIR)$(bindir)
	$(LTINSTALL) sqlite3$(BEXE) $(DESTDIR)$(bindir)
	$(INSTALL) -d $(DESTDIR)$(includedir)
	$(INSTALL) -m 0644 sqlite3.h $(DESTDIR)$(includedir)
	$(INSTALL) -m 0644 $(TOP)/src/sqlite3ext.h $(DESTDIR)$(includedir)
	$(INSTALL) -d $(DESTDIR)$(pkgconfigdir)
	$(INSTALL) -m 0644 sqlite3.pc $(DESTDIR)$(pkgconfigdir)

pkgIndex.tcl:
	echo 'package ifneeded sqlite3 $(RELEASE) [list load $(TCLLIBDIR)/libtclsqlite3.so sqlite3]' > $@
tcl_install:	lib_install libtclsqlite3.la pkgIndex.tcl
	$(INSTALL) -d $(DESTDIR)$(TCLLIBDIR)
	$(LTINSTALL) libtclsqlite3.la $(DESTDIR)$(TCLLIBDIR)
	rm -f $(DESTDIR)$(TCLLIBDIR)/libtclsqlite3.la $(DESTDIR)$(TCLLIBDIR)/libtclsqlite3.a
	$(INSTALL) -m 0644 pkgIndex.tcl $(DESTDIR)$(TCLLIBDIR)

clean:	
	rm -f *.lo *.la *.o sqlite3$(TEXE) libsqlite3.la
	rm -f sqlite3.h opcodes.*
	rm -rf .libs .deps
	rm -f lemon$(BEXE) lempar.c parse.* sqlite*.tar.gz
	rm -f mkkeywordhash$(BEXE) keywordhash.h
	rm -f $(PUBLISH)
	rm -f *.da *.bb *.bbg gmon.out
	rm -rf tsrc .target_source
	rm -f tclsqlite3$(TEXE)
	rm -f testfixture$(TEXE) test.db
	rm -f sqlite3.dll sqlite3.lib sqlite3.exp sqlite3.def
	rm -f sqlite3.c
	rm -f sqlite3_analyzer$(TEXE) sqlite3_analyzer.c

distclean:	clean
	rm -f config.log config.status libtool Makefile sqlite3.pc

#
# Windows section
#
dll: sqlite3.dll

REAL_LIBOBJ = $(LIBOBJ:%.lo=.libs/%.o)

$(REAL_LIBOBJ): $(LIBOBJ)

sqlite3.def: $(REAL_LIBOBJ)
	echo 'EXPORTS' >sqlite3.def
	nm $(REAL_LIBOBJ) | grep ' T ' | grep ' _sqlite3_' \
		| sed 's/^.* _//' >>sqlite3.def

sqlite3.dll: $(REAL_LIBOBJ) sqlite3.def
	$(TCC) -shared -o $@ sqlite3.def \
		-Wl,"--strip-all" $(REAL_LIBOBJ)
