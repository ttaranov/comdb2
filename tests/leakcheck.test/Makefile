include $(TESTSROOTDIR)/testcase.mk
include $(TESTSROOTDIR)/../main.mk
export TEST_TIMEOUT=6m
CFLAGS+=-I$(SRCHOME)/cdb2api -I$(SRCHOME)/bbinc
CFLAGS+=-D_GNU_SOURCE

# Oh hi references:
# sqlcache.c -> time_epochms() -> logmsg() -> segtok() -> segstring.o -> tokdup() -> per-subsystem malloc() -> dlmalloc().
CDB2LIBS=$(SYSPATH) -L$(SRCHOME)/cdb2api -l:libcdb2api.a -L$(SRCHOME)/protobuf/ -lcdb2protobuf -lprotobuf-c -lpthread -L$(SRCHOME)/bb -lbb -L$(SRCHOME)/dlmalloc -ldlmalloc -lssl -lcrypto

tool:
	make sqlcache

sqlcache: sqlcache.o
	$(CC) -o $@ $< $(CDB2LIBS) 
	
%.o: %.c
	echo $(CC) -o $@ -c $< $(CFLAGS) 
	$(CC) -o $@ -c $< $(CFLAGS) 
