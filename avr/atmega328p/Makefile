###############################################################################
# Makefile for the project testavr
###############################################################################

## General Flags
PROJECT = testavr
MCU = atmega328p
TARGET = testavr
CC = avr-gcc

#CPP = avr-g++

## Options common to compile, link and assembly rules
COMMON = -mmcu=$(MCU)

## Compile options common for all C compilation units.
CFLAGS = $(COMMON)
CFLAGS += -Wall -gdwarf-2 -O0 -std=gnu99 -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums
CFLAGS += -MD -MP -MT gcc/$(*F).o -MF gcc/$(@F).d 

## Linker flags
LDFLAGS = $(COMMON)
LDFLAGS +=  -Wl,-Map=gcc/testavr.map


## Intel Hex file production flags
HEX_FLASH_FLAGS = -R .eeprom -R .fuse -R .lock -R .signature

HEX_EEPROM_FLAGS = -j .eeprom
HEX_EEPROM_FLAGS += --set-section-flags=.eeprom="alloc,load"
HEX_EEPROM_FLAGS += --change-section-lma .eeprom=0 --no-change-warnings


## Objects that must be built in order to link
OBJECTS = gcc/testavr.o 

## Objects explicitly added by the user
LINKONLYOBJECTS = 

## Build
all: $(TARGET).elf testavr.hex gcc/testavr.eep gcc/testavr.lss
#size

## Compile
gcc/testavr.o: testavr.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $< -o $@

##Link
$(TARGET).elf: $(OBJECTS)
	 $(CC) $(LDFLAGS) $(OBJECTS) $(LINKONLYOBJECTS) $(LIBDIRS) $(LIBS) -o $(TARGET).elf

%.hex: $(TARGET).elf
	avr-objcopy -O ihex $(HEX_FLASH_FLAGS)  $< $@

gcc/%.eep: $(TARGET).elf
	-avr-objcopy $(HEX_EEPROM_FLAGS) -O ihex $< $@ || exit 0

gcc/%.lss: $(TARGET).elf
	avr-objdump -h -S $< > $@

size: ${TARGET}
	@echo
	avr-size -C --mcu=${MCU} ${TARGET}

## Clean target
.PHONY: clean
clean:
	-rm -rf $(OBJECTS) $(TARGET).elf $(TARGET).hex gcc/*
#	$(TARGET).eep $(TARGET).lss $(TARGET).map


## Other dependencies
-include $(shell mkdir gcc 2>/dev/null) $(wildcard dep/*)

