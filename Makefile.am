AUTOMAKE_OPTIONS = foreign

ACLOCAL_AMFLAGS = -I m4

bin_PROGRAMS = cava
cava_SOURCES = cava.c cavacore.c config.c input/common.c \
               output/terminal_noncurses.c output/raw.c output/noritake.c
cava_CPPFLAGS = -DPACKAGE=\"$(PACKAGE)\" -DVERSION=\"$(VERSION)\" \
           -D_POSIX_SOURCE -D_POSIX_C_SOURCE=200809L -D_XOPEN_SOURCE_EXTENDED \
	   -DFONTDIR=\"@FONT_DIR@\"
cava_CFLAGS = -std=c99 -Wall -Wextra -Wno-unused-result -Wno-maybe-uninitialized -Wno-vla-parameter
cava_LDADD =

if WINDOWS
    cava_CFLAGS += -D_MSC_VER
    cava_LDADD += -luser32 -lkernel32 -lOle32
    cava_LDFLAGS = -Wl,--allow-multiple-definition
    cava_SOURCES += input/winscap.c
else
    cava_SOURCES += input/fifo.c input/shmem.c
endif

if OSX
    cava_CFLAGS += -DNORT
else
    cava_font_dir = @FONT_DIR@
    cava_font__DATA = cava.psf
endif

if LINUX
    cava_LDADD += -lrt
endif

if ALSA
    cava_SOURCES += input/alsa.c
endif

if PORTAUDIO
    cava_SOURCES += input/portaudio.c
endif

if PIPEWIRE
    cava_SOURCES += input/pipewire.c
endif

if PULSE
    cava_SOURCES += input/pulse.c
endif

if SNDIO
    cava_SOURCES += input/sndio.c
endif

if NCURSES
    cava_SOURCES += output/terminal_ncurses.c
endif

if SDL
    cava_SOURCES += output/sdl_cava.c
endif

if SDL_GLSL
    cava_SOURCES += output/sdl_glsl.c
endif
