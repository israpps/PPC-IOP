BUILD_SCRIPTS := $(abspath $(CURDIR)/../buildscripts)
PATCH_DIR := $(abspath $(CURDIR)/../patch)

BUILD ?= ELF

EE_ASM_DIR = asm/
ifeq ($(BUILD),LIB)
EE_LIB = libppcpatch.a
EE_CFLAGS += -DBUILDING_LIB
else
EE_BIN = PPC_PATCH_LOADER.ELF
endif
EE_OBJS = patch_loader.o patch.o

EE_LDFLAGS = -L$(PS2SDK)/ee/lib -nostartfiles -lc -lm -lkernel -Wl,-zmax-page-size=128 

BIN2S = $(PS2SDK)/bin/bin2s

#prep patch before building patch_loader
all::
	@mkdir -p asm
	$(PPC_TOOL_PREFIX)objcopy -O binary $(PATCH_DIR)/bin/patch.elf $(PATCH_DIR)/bin/patch.bin
	$(BIN2S) $(PATCH_DIR)/bin/patch.bin asm/patch.s patch_bin

	$(MAKE) $(EE_BIN)

clean::
	rm -f asm/*
	rm -f *.map

include $(PS2SDK)/samples/Makefile.pref
include $(BUILD_SCRIPTS)/ppc/Defs.make
include $(BUILD_SCRIPTS)/ee/Rules.bin.make
include $(BUILD_SCRIPTS)/ee/Rules.make
