TARGET = stage1
OBJS = start.o stage1.o

CC = gcc
OBJCOPY = objcopy
CFLAGS = -DSMP -isystem ../freebsd-headers/include -Wl,--build-id=none -Os -fno-stack-protector -fpic -fpie
LDFLAGS = -T linker.ld -nostartfiles -nostdlib

ifneq ($(filter $(FW), 700 701 702 750 751 755 800 801 803 850 852 900 903 904 950 951 960 1000 1001 1050 1070 1071 1100),)
CFLAGS += -DFIRMWARE=$(FW)
else
$(error "Invalid firmware")
endif

all: $(TARGET).bin

%.bin: %.elf
	$(OBJCOPY) -S -O binary $^ $@

$(TARGET).elf: $(OBJS)
	$(CC) $(CFLAGS) $^ -o $@ $(LDFLAGS)

clean:
	@rm -f $(TARGET).bin $(TARGET).elf $(OBJS)
