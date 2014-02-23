#MAKEFILE for the stm32f4discovery

#Target Name
TARGET = output
#Source files
SOURCES = main.c
#Location of something
WARE = 

#tools
FLASH = lmflash -q ek-lm4f120xl -r
CC = arm-none-eabi-gcc
OBJCOPY = arm-none-eabi-objcopy
LD = arm-none-eabi-ld
AR = arm-none-eabi-ar


CFLAGS += -mcpu=cortex-m4
CFLAGS += -mthumb
CFLAGS += -Wall
CFLAGS += -ffunction-sections
CFLAGS += -g
CFLAGS += -Os
CFLAGS += -DSTM32F407VG
CFLAGS += -DSTM32F4XX
CFLAGS += -DUSE_STDPERIPH_DRIVER
CFLAGS += -D__FPU_USED
CFLAGS += -D__ASSEMBLY__
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\CoOS\kernel
CFLAGS += -IC:\Users\Christian\R2DB\svn
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\r2db_brain
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\r2db_tasks
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\CoOS\Other
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\r2db_parts
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\cmsis_lib
CFLAGS += -IC:\Users\Christian\R2DB
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\cmsis_lib\include
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\cmsis_boot
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\CoOS\portable
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\cmsis
CFLAGS += -IC:\Users\Christian\R2DB\svn\dev\CoOS

LDFLAGS += -mcpu=cortex-m4
LDFLAGS += -mthumb
LDFLAGS += -nostartfiles
LDFLAGS += -Wl,-Map=STM32F4_Discovery_CoOS.map
LDFLAGS += -Os
LDFLAGS += -Wl,--gc-sections
LDFLAGS += -LC:\CooCox\CoIDE\configuration\ProgramData\STM32F4_Discovery_CoOS
LDFLAGS += -Wl,-TC:\CooCox\CoIDE\configuration\ProgramData\STM32F4_Discovery_CoOS/arm-gcc-link.ld
LDFLAGS += -g
LDFLAGS += -L..\..\..
LDFLAGS += -lm


#compiler
%.o: %.c
	arm-none-eabi-gcc $(CFLAGS) -c $(<) -o $(@) 
	
{target}.elf: $(OBJECTS)
	arm-none-eabi-gcc $(LDFLAGS) -o $(@) $(<)  