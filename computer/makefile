#Compiler
CC=gcc

##FLAGS
#CFLAGS compiler flags, os flags will be appended to this
CFLAGS=-Wall
#LFLAGS linker flags, os flags will be appended to this
LFLAGS=
#WINDOWS FLAGS
WIN_OS=-fopenmp
#MAC OS X FLAGS
MAC_OS=
#OHTER OS FLAGS
OTHER_OS=-fopenmp
#PROFILER FLAGS
PROFILER=-pg# -v

#SOURCE FILES
SOURCES=main.c filehandler.c memhandler.c linkedlist.c ui.c

#NAME without extention
EXECUTABLE=opdracht



## DETECTING OS
ifdef SystemRoot
#windows
	RM=del
	EXT=.exe
	CFLAGS += $(WIN_OS)
else
#unix
	RM=rm
	EXT=
	UNAME_S := $(shell uname -s)
	ifeq ($(UNAME_S),Darwin) #MAC OS
		CFLAGS += $(MAC_OS)
	else # other
		CFLAGS += $(OTHER_OS)
	endif
endif

# OBJECT USING BY FILES
OBJECTS=$(SOURCES:.c=.o)

help:
	@echo "Make for CXX"
	@echo "Made by Christian van Meggelen"
	@echo "and Sander van Schaick"
	@echo ""
	@echo "usage:"
	@echo "make [args]"
	@echo "'all'		: compile sources and make executable"
	@echo "'build'		: same as 'all' but also run the executable"
	@echo "'rebuild'	: remove the executable and all object files, compile sources and make executable"
	@echo "'rebuild2'	: same as 'rebuild' but always use the 'rm' function"
	@echo "'run'		: run the executable"
	@echo "'profiler'	: same as rebuild but use the $(PROFILER) tag, run the executable and use gprof to get an output"
	@echo "'clean'		: remove the executable and all object files"
	@echo "'clean2'	: same as 'clean' but always use the 'rm' function"
	@echo "'clc'		: remove all object files"
	@echo "'clc2'		: same as 'clc' but always use the 'rm' function"

all: output

build: output run

run:
	./$(EXECUTABLE)$(EXT)

#rebuilding
rebuild: cleanignored output
rebuild2: clean2ignored output

#profiling linking
profilingthing: cleanignored $(OBJECTS)
	$(CC) $(LFLAGS) $(PROFILER) $(OBJECTS) -o $(EXECUTABLE)$(EXT)

profiler: profilingthing run
	gprof $(EXECUTABLE)$(EXT) gmon.out > profiler.txt

#the linker
output: $(OBJECTS)
	$(CC) $(LFLAGS) $(OBJECTS) -o $(EXECUTABLE)$(EXT)
#object genaration
.c.o:
	$(CC) -c $(CFLAGS) $< -o $@



#cleaning functions
clean:
	$(RM) *.o $(EXECUTABLE)$(EXT)
cleanignored:
	-$(RM) *.o $(EXECUTABLE)$(EXT)
clean2:
	rm *.o $(EXECUTABLE)$(EXT)
clean2ignored:
	-rm *.o $(EXECUTABLE)$(EXT)
clc:
	$(RM) *.o
clc2:
	rm *.o
