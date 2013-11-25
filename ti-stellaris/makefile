#MAKEFILE for the ti-stellaris

#Target Name
TARGET = output
#Source files
SOURCES = main.c
#Location of StallarisWare
STALLARISWARE = $(HOME)/Library/StellarisWare
#Path to Linker Script
LINKSCRIPT = start.ld

#tools
FLASH = lm4flash
CC = arm-none-eabi-gcc
OBJCOPY = arm-none-eabi-objcopy
LD = arm-none-eabi-ld
AR = arm-none-eabi-ar

#Compiler flags
CFLAGS += -mthumb					#Using the Thumb Instruction Set
CFLAGS += -mcpu=cortex-m4			#The CPU Variant
CFLAGS += -mfloat-abi=softfp		#Which floating point ABI to use
CFLAGS += -mfpu=fpv4-sp-d16			#The type of FPU we are using
CFLAGS += -Os						#Compile with Size Optimizations
CFLAGS += -ffunction-sections		#Create a separate function section
CFLAGS += -fdata-sections			#Create a separate data section
CFLAGS += -MD						#Create dependency files (*.d)
CFLAGS += -std=c99					#Comply with C99
CFLAGS += -Wall						#Enable All Warnings 
CFLAGS += -pedantic					#More ANSI Checks
CFLAGS += -Dgcc						#Flag used in driverlib for compiler specific flags
CFLAGS += -DPART_LM4F120H5QR		#Flag used in driverlib for specifying the silicon version.
CFLAGS += -I$(STALLARISWARE)		#Include StellarisWare
#CFLAGS += -DTARGET_IS_BLIZZARD_RA1	#Used in driverlib to determine what is loaded in rom.

#Linker flags
LDFLAGS += --gc-sections			#Tell the linker to ignore functions that aren't used.
LDFLAGS += -T $(LINKSCRIPT)			#Path to Linker Script
LDFLAGS += --entry ResetISR			#Name of the application entry point

#Get the name of the objects
SOURCES += startup_gcc.c
OBJECTS = $(SOURCES:%.c=build/%.o)
#END OWN

#copied vars from MAKEDEF
#
# Get the location of libgcc.a from the GCC front-end.
#
LIBGCC=$(shell $(CC) $(CFLAGS) -print-libgcc-file-name)

#
# Get the location of libc.a from the GCC front-end.
#
LIBC=$(shell $(CC) $(CFLAGS) -print-file-name=libc.a)

#
# Get the location of libm.a from the GCC front-end.
#
LIBM=$(shell $(CC) $(CFLAGS) -print-file-name=libm.a)
#END MAKEDEF

#default target
all: $(TARGET).axf

#make the output dir
${COMPILER}:
	@mkdir -p build

.PHONY: clean flash
#Flash th
flash: $(TARGET).bin
	$(FLASH) $(TARGET).bin

#Clean the build	
clean:
	-rm -rf build

	
#Include automatically generated dependency files.
ifneq ($(MAKECMDGOALS),clean)
-include $(wildcard build/*.d) __dummy__
endif

#Compiler
build/%.o: %.c
	$(CC) -c $(CFLAGS) -o $(@) $(<)

#Linker
build/${TARGET}.axf: $(OBJECTS) $(LINKSCRIPT)
	$(LD) $(LDFLAGS) -o $(TARGET).axf $(OBJECTS) '$(LIBM)' '$(LIBC)' '$(LIBGCC)'

#binary file
build/${TARGET}.bin: build/$(TARGET).axf
	$(OBJCOPY) -O binary $(@) $(<)