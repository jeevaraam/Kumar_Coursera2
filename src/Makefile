#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# <Put a Description Here>
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      <Put a description of the supported targets here>
#
# Platform Overrides:
#      <Put a description of the supported Overrides here
#
#------------------------------------------------------------------------------
include sources.mk

# Platform Overrides
PLATFORM ?= HOST

FLAGS = -Wall -Werror -g -O0 -std=c99

# Architectures Specific Flags

LINKER_FILE = ../msp432p401r.lds
CPU = cortex-m4
ARCH = thumb
SPECS = nosys.specs

TARGET = c1m2
CPPFLAGS = -D$(PLATFORM)

# Compiler Flags and Defines
ifeq ($(PLATFORM),MSP432)
	CC = arm-none-eabi-gcc
	LD = arm-none-eabi-ld
	LDFLAGS = -Wl,-Map=$(TARGET).map -T $(LINKER_FILE)
	CFLAGS = $(CPPFLAGS) -mcpu=$(CPU) -m$(ARCH) -march=armv7e-m -mfloat-abi=hard -mfpu=fpv4-sp-d16 -mfpu=fpv4-sp-d16 --specs=$(SPECS) $(FLAGS)
else
	CC = gcc
	LD = ld
	LDFLAGS = -Wl,-Map=$(TARGET).map
	CFLAGS = $(CPPFLAGS) $(FLAGS)	
endif

OBJS = $(SOURCES:.c=.o)
DEBS = $(SOURCES:.c=.d)

.PHONY: compile-all
compile-all:$(OBJS)

%.o : %.c
	$(CC) $(INCLUDES) -c $< $(CFLAGS) -o $@

%.asm : %.c
	$(CC) $(INCLUDES) -S $< $(CFLAGS) -o $@

%.i : %.c
	$(CC) $(INCLUDES) -E $< $(CFLAGS) -o $@

%.d : %.c
	$(CC) $(INCLUDES) -M $< $(CFLAGS) -o $@

.PHONY: build
build: $(DEBS) $(TARGET).out

$(TARGET).out:$(OBJS) 
	$(CC) $(INCLUDES) $(OBJS) $(CFLAGS) $(LDFLAGS) -o $@


.PHONY: clean
clean:
	rm -f $(OBJS) $(TARGET).out $(TARGET).map $(SOURCES:.c=.i) $(SOURCES:.c=.asm) $(SOURCES:.c=.d)
