# You know, there are pre-compile DEBs of this...
NDK_KIT = ../../android-ndk-r9d/
BIN = $(NDK_KIT)toolchains/arm-linux-androideabi-4.6/prebuilt/linux-x86/bin/
PLATF_KIT = platforms/android-15/
ARM_INC = $(NDK_KIT)$(PLATF_KIT)arch-arm/usr/include
INC_EXTRA = ../android-inlude-extras
ARM_LIB = $(NDK_KIT)$(PLATF_KIT)arch-arm/usr/lib
LIB_EXTRA = ../android-lib-extras
PREFIX = arm-linux-androideabi-

AR = $(BIN)$(PREFIX)ar
AS = $(BIN)$(PREFIX)as
CC = $(BIN)$(PREFIX)gcc
CXX = $(BIN)$(PREFIX)c++
LD = $(BIN)$(PREFIX)ld

CXX ?= g++
INCS = -I$(ARM_INC) -I$(INC_EXTRA)
CXXFLAGS ?= -O2 -Wall $(INCS)
LDFLAGS += -Wl,-Bsymbolic-functions -Wl,--dynamic-linker,/system/bin/linker \
		-Wl,-rpath,/system/lib -Wl,-rpath,$(ARM_LIB) -Wl,-rpath-link,$(ARM_LIB) \
        --sysroot=$(NDK_KIT)$(PLATF_KIT)arch-arm/ \
		-Wl,-L$(ARM_LIB) -L$(LIB_EXTRA)

GASIA_GAMEPAD_HACKS = true

ifeq ($(GASIA_GAMEPAD_HACKS),true)
CXXFLAGS += -DGASIA_GAMEPAD_HACKS
endif

all: sixad_bins

sixad_bins:
	mkdir -p bins
	$(CXX) $(CXXFLAGS) $(LDFLAGS) sixad-bin.cpp bluetooth.cpp shared.cpp textfile.cpp __ppoll.S poll.cpp __set_errno.cpp -o bins/sixad-bin -lc -lbluetooth -fpermissive
	$(CXX) $(CXXFLAGS) $(LDFLAGS) sixad-sixaxis.cpp sixaxis.cpp shared.cpp uinput.cpp textfile.cpp __ppoll.S poll.cpp __set_errno.cpp -o bins/sixad-sixaxis -lc

clean:
	rm -f *~ bins/*

