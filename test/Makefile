##
## DO NOT EDIT THIS FILE
## 
## Edit "setting.mak"
## To create the settings file use: "make settings"
##

#Target Name
TARGET = output
#Source files
SOURCES = main.c
#Location of StellarisWare
STELLARISWARE = $(HOME)/Library/StellarisWare
#Path to Linker Script
LINKSCRIPT = link.ld

#tools
FLASH = lm4flash
CC = arm-none-eabi-gcc
AS = arm-none-eabi-gcc
OBJCOPY = arm-none-eabi-objcopy
LD = arm-none-eabi-ld
AR = arm-none-eabi-ar


all:
	@echo "Testing makefile"

PHONY: settings

settings: settings.mak

settings.mak:
	@echo "Creating settings.mak"
	@echo "#Target Name\nTARGET = $(TARGET)\n#Location of StellarisWare\nSTELLARISWARE = $(STELLARISWARE)\n#tools\nFLASH = $(FLASH)\nCC = $(CC)\nAS = $(AS)\nOBJCOPY = $(OBJCOPY)\nLD = $(LD)\nAR = $(AR)" > settings.mak
	@echo "#Target1" > settings3.mak
	@echo "#Target2" >> settings3.mak
	@echo "Done creating settings.mak"
