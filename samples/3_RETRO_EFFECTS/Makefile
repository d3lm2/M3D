PSPSDK=$(shell psp-config --pspsdk-path)
TARGET = RETRO_EFFECTS
OBJS = main.o

INCDIR = $(PSPSDK)/include
CFLAGS = -O2 -G0 -Wall
CXXFLAGS = $(CFLAGS) -fno-exceptions -fno-rtti
ASFLAGS = $(CFLAGS)

LIBDIR = $(PSPSDK)/lib
LDFLAGS = 
LIBS = -lpspjpeg -lpspmpeg -lpspkernel -lmikmod -lpng -lM3D -lm -lz -lpsphprm -lpspsdk -lpspctrl -lpspumd -lpsprtc -lpsppower -lpspgu -lpspgum \
		-lpspaudiolib -lpspaudio -lpspaudiocodec -lpsphttp -lpspssl -lpspwlan -lpspnet_adhocmatching \
		-lpspnet_adhoc -lpspnet_adhocctl -lstdc++ -lpspmpegbase
		
PSP_FW_VERSION = 660

EXTRA_TARGETS = EBOOT.PBP
PSP_EBOOT_TITLE = "RETRO EFFECTS"
PSP_EBOOT_ICON = ../00_ICONS/ICON0.PNG

include $(PSPSDK)/lib/build.mak
