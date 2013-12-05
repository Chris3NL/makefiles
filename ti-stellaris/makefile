#MAKEFILE for the ti-stellaris

#Target Name
TARGET = output
#Source files
SOURCES = main.c
#Location of StallarisWare
STALLARISWARE = $(HOME)/Library/StellarisWare
#Path to Linker Script
LINKSCRIPT = start.ld

##
##tools
##
FLASH = lm4flash
CC = arm-none-eabi-gcc
OBJCOPY = arm-none-eabi-objcopy
LD = arm-none-eabi-ld
AR = arm-none-eabi-ar
RM = rm -rf
##
##Compiler flags
##

#Using the Thumb Instruction Set
CFLAGS += -mthumb
#The CPU Variant
CFLAGS += -mcpu=cortex-m4
#Which floating point ABI to use
CFLAGS += -mfloat-abi=softfp
#The type of FPU we are using
CFLAGS += -mfpu=fpv4-sp-d16
#Compile with Size Optimizations <disabled for using interrupts>
#CFLAGS += -Os
#Create a separate function section
CFLAGS += -ffunction-sections
#Create a separate data section
CFLAGS += -fdata-sections
#Create dependency files (*.d)
CFLAGS += -MD
#Comply with C99
CFLAGS += -std=c99
#Enable All Warnings 
CFLAGS += -Wall
#More ANSI Checks
CFLAGS += -pedantic
#Flag used in driverlib for compiler specific flags
CFLAGS += -Dgcc
#Flag used in driverlib for specifying the silicon version.
CFLAGS += -DPART_LM4F120H5QR
#Include StellarisWare
CFLAGS += -I$(STALLARISWARE)
#Used in driverlib to determine what is loaded in rom.
#CFLAGS += -DTARGET_IS_BLIZZARD_RA1

##
##Linker flags
##

#Tell the linker to ignore functions that aren't used.
LDFLAGS += --gc-sections
#Path to Linker Script
LDFLAGS += -T $(LINKSCRIPT)
#Name of the application entry point
LDFLAGS += --entry ResetISR

##
##Automatic part
##

#Get the name of the objects
SOURCES += startup_gcc.c
OBJECTS = $(SOURCES:%.c=build/%.o)


#Get the location of libgcc.a from the GCC front-end.
LIBGCC=$(shell $(CC) $(CFLAGS) -print-libgcc-file-name)

#Get the location of libc.a from the GCC front-end.
LIBC=$(shell $(CC) $(CFLAGS) -print-file-name=libc.a)

#Get the location of libm.a from the GCC front-end.
LIBM=$(shell $(CC) $(CFLAGS) -print-file-name=libm.a)

#default target
all: build build/$(TARGET).axf build/$(TARGET).bin

#make the output dir
build:
	@mkdir -p build

.PHONY: clean flash
#Flash the Stellaris
flash: build/$(TARGET).bin
	$(FLASH) $(<)

#Clean the build	
clean:
	-$(RM) build

	
#Include automatically generated dependency files.
ifneq ($(MAKECMDGOALS),clean)
-include $(wildcard build/*.d) __dummy__
endif

#Compiler
build/%.o: %.c
	$(CC) -c $(CFLAGS) -o $(@) $(<)

#Linker
build/${TARGET}.axf: $(OBJECTS) $(LINKSCRIPT)
	$(LD) $(LDFLAGS) -o $(@) $(OBJECTS) '$(LIBM)' '$(LIBC)' '$(LIBGCC)'

#binary file
build/${TARGET}.bin: build/$(TARGET).axf
	$(OBJCOPY) -O binary $(<) $(@)
