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
PLATFORM =$(PLATFORM) 

FLAGS = -Wall -Werror -g -O0 -std=c99

# Architectures Specific Flags
LINKER_FILE = msp432p401r.lds
CPU = cortex-m4
ARCH = thumb
SPECS = nosys.specs

LDFLAGS = -Wl, -Map=$(BASENAME).map
CPPFLAGs = $(PLATFORM)

# Compiler Flags and Defines
ifeq($(PLATFORM),MSP432)
	CC = arm-none-eabi-gcc
	LD = arm-none-eabi-ld	
	CFLAGS = -mcpu=$(CPU) -m$(ARCH) --specs=$(SPECS) -march=armv7e-m -mfloat-abi=hard -mfpu=fpv4-sp-d16 -T $(LINKER_FILE)
else
	cc=gcc
	LD=ld
endif

OBJS=$(SRCS:.c=.o)

%.o : %.c
	$(CC) -c
