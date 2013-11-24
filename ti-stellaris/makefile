
#OWN vars
SOURCES=main.c
STALLARISWARE=$(HOME)/Library/StellarisWare
#END OWN

#copied vars from Makefile (BLINKY)

#
# Defines the part type that this project uses.
#
PART=LM4F120H5QR

#
# Set the processor variant.
#
VARIANT=cm4f
#END BLINKY

#copied vars from MAKEDEF
CPU=-mcpu=cortex-m4
FPU=-mfpu=fpv4-sp-d16 -mfloat-abi=softfp
#
# The flags passed to the assembler.
#
AFLAGS=-mthumb \
       ${CPU}  \
       ${FPU}  \
       -MD

#
# The flags passed to the compiler.
#
CFLAGS=-mthumb             \
       ${CPU}              \
       ${FPU}              \
       -Os                 \
       -ffunction-sections \
       -fdata-sections     \
       -MD                 \
       -std=c99            \
       -Wall               \
       -pedantic           \
       -DPART_${PART}      \
       -c				   \
	   -Dgcc
#
# The command for calling the library archiver.
#
AR=arm-none-eabi-ar

#
# The command for calling the linker.
#
LD=arm-none-eabi-ld

#
# The flags passed to the linker.
#
LDFLAGS=--gc-sections

#
# Get the location of libgcc.a from the GCC front-end.
#
LIBGCC=${shell ${CC} ${CFLAGS} -print-libgcc-file-name}

#
# Get the location of libc.a from the GCC front-end.
#
LIBC=${shell ${CC} ${CFLAGS} -print-file-name=libc.a}

#
# Get the location of libm.a from the GCC front-end.
#
LIBM=${shell ${CC} ${CFLAGS} -print-file-name=libm.a}

#
# The command for extracting images from the linked executables.
#
OBJCOPY=${PREFIX}-objcopy
#END MAKEDEF

#copied vars from WEB1: http://eehusky.wordpress.com/2012/12/04/using-gcc-with-ti-stellaris-launchpad-a-more-in-depth-look/ #used in MAKEDEF
#CFLAGS += -mthumb                  #Using the Thumb Instruction Set
#CFLAGS += -mcpu=cortex-m4          #The CPU Variant
#CFLAGS += -mfloat-abi=softfp       #Which floating point ABI to use
#CFLAGS += -mfpu=fpv4-sp-d16        #The type of FPU we are using
#CFLAGS += -Os                      #Compile with Size Optimizations
#CFLAGS += -ffunction-sections      #Create a separate function section
#CFLAGS += -fdata-sections          #Create a separate data section
#CFLAGS += -MD                      #Create dependency files (*.d)
#CFLAGS += -std=c99                 #Comply with C99
#CFLAGS += -Wall                    #Enable All Warnings 
#CFLAGS += -pedantic                #More ANSI Checks
#CFLAGS += -Dgcc                    #Flag used in driverlib for compiler specific flags
#CFLAGS += -DPART_LM4F120H5QR       #Flag used in driverlib for specifying the silicon version.
CFLAGS += -DTARGET_IS_BLIZZARD_RA1 #Used in driverlib to determine what is loaded in rom.

LDFLAGS    += -T blinky.ld              #Path to Linker Script
LDFLAGS    += --entry ResetISR          #Name of the application entry point
#LDFLAGS    += --gc-sections             #Tell the linker to ignore functions that aren't used.
#END WEB1


all:
	arm-none-eabi-gcc main.c startup_gcc.c -g -mthumb -mcpu=cortex-m4 -mfpu=fpv4-sp-d16 -mfloat-abi=softfp -Os -ffunction-sections -fdata-sections -MD -std=c99 -Wall -pedantic -DPART_LM4F120H5QR -c -I$(HOME)/Library/StellarisWare  -DTARGET_IS_BLIZZARD_RA1
	arm-none-eabi-ld -T start.ld --entry ResetISR -o a.out startup_gcc.o main.o --gc-sections
	arm-none-eabi-objcopy -O binary a.out main.bin

flash: all
	lm4flash main.bin

.PHONY: clean
clean:
	-rm *.o *.d *.out *.bin

#compiler
	arm-none-eabi-gcc
	main.c startup_gcc.c
	-g
	-mthumb
	-mcpu=cortex-m4
	-mfpu=fpv4-sp-d16
	-mfloat-abi=softfp
	-Os
	-ffunction-sections
	-fdata-sections
	-MD
	-std=c99
	-Wall
	-pedantic
	-DPART_LM4F120H5QR
	-c
	-I$(STALLARISWARE)
	-DTARGET_IS_BLIZZARD_RA1
	
#linker
	arm-none-eabi-ld
	-T
	start.ld
	--entry ResetISR
	-o
	a.out
	startup_gcc.o main.o
	--gc-sections