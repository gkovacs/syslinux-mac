## -----------------------------------------------------------------------
##
##   Copyright 2001-2008 H. Peter Anvin - All Rights Reserved
##
##   This program is free software; you can redistribute it and/or modify
##   it under the terms of the GNU General Public License as published by
##   the Free Software Foundation, Inc., 53 Temple Place Ste 330,
##   Boston MA 02111-1307, USA; either version 2 of the License, or
##   (at your option) any later version; incorporated herein by reference.
##
## -----------------------------------------------------------------------

##
## Linux FAT installer
##

topdir = ..
include $(topdir)/MCONFIG



OPTFLAGS = -g -O0 -Dalloca=malloc
INCLUDES = -I. -I.. -I../libinstaller -I../libfat
CFLAGS	 = $(GCCWARN) -D_FILE_OFFSET_BITS=64 $(OPTFLAGS) $(INCLUDES)
LDFLAGS	 = 

SRCS     = syslinux.c \
	   ../libinstaller/syslxopt.c \
	   ../libinstaller/syslxcom.c \
	   ../libinstaller/setadv.c \
	   ../libinstaller/advio.c \
           ../libinstaller/fat.c \
           ../libinstaller/syslxmod.c \
	   ../libinstaller/bootsect_bin.c \
	   ../libinstaller/ldlinux_bin.c \
	   ../libfat/cache.c \
	   ../libfat/fatchain.c \
	   ../libfat/open.c \
	   ../libfat/searchdir.c
OBJS	 = $(patsubst %.c,%.o,$(notdir $(SRCS)))

.SUFFIXES: .c .o .i .s .S

VPATH = .:../libinstaller

all: installer

tidy dist:
	-rm -f *.o *.i *.s *.a .*.d *.tmp

clean: tidy
	-rm -f syslinux syslinux-nomtools

spotless: clean
	-rm -f *~

installer: syslinux syslinux-nomtools

syslinux: $(OBJS)
	$(CC) $(LDFLAGS) -o $@ $^

syslinux-nomtools: syslinux
	ln -f $< $@

%.o: %.c
	$(CC) $(UMAKEDEPS) $(CFLAGS) -c -o $@ $<
%.i: %.c
	$(CC) $(UMAKEDEPS) $(CFLAGS) -E -o $@ $<
%.s: %.c
	$(CC) $(UMAKEDEPS) $(CFLAGS) -S -o $@ $<

-include .*.d *.tmp
