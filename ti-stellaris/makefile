all:
	arm-none-eabi-gcc main.c startup_gcc.c -g -mthumb -mcpu=cortex-m4 -mfpu=fpv4-sp-d16 -mfloat-abi=softfp -Os -ffunction-sections -fdata-sections -MD -std=c99 -Wall -pedantic -DPART_LM4F120H5QR -c -I$(HOME)/Library/StellarisWare  -DTARGET_IS_BLIZZARD_RA1
	arm-none-eabi-ld -T start.ld --entry ResetISR -o a.out startup_gcc.o main.o --gc-sections
	arm-none-eabi-objcopy -O binary a.out main.bin

flash: all
	lm4flash main.bin
