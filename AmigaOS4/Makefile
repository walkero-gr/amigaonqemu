# This is a makefile to boot the AmigaOS 4 on an emulated SAM 460ex
#
# You can override any parameter like shown below 
# make CD=
# make CD=amigaos4.1fe_updates.iso
# make newhd HDNAME=test HDSIZE=100M

# Change CD inside qemu
# (qemu) eject -f cd
# (qemu) change cd ./Sam460InstallCD-53.58.iso

MACHINE := sam460ex
MEM ?= 2048
HD ?= hd0.qcow2
CD ?= Sam460InstallCD-53.58.iso
HDNAME ?= hd0
HDSIZE ?= 255M

ifneq ($(strip $(CD)),)
	CDDEV = -drive if=none,id=cd,file=$(CD),format=raw -device ide-cd,drive=cd,bus=ide.1
else
	CDDEV = -drive if=none,id=cd -device ide-cd,drive=cd,bus=ide.1
endif

.PHONY: boothd bootcd newhd

default: boothd

boothd:
	@qemu-system-ppc -machine $(MACHINE) -m $(MEM) \
		$(CDDEV) \
		-drive if=none,id=hd,file=$(HD),format=qcow2 -device ide-hd,drive=hd,bus=ide.0 \
		-boot order=c,menu=on \
		-rtc base=localtime \
		-device rtl8139,netdev=mynet0 -netdev user,id=mynet0 -device es1370

bootcd:
	@qemu-system-ppc -machine $(MACHINE) -m $(MEM) \
		-drive if=none,id=hd,file=$(HD),format=qcow2 -device ide-hd,drive=hd,bus=ide.0 -boot c \
		-drive if=none,id=cd,file=$(CD),format=raw -device ide-cd,drive=cd,bus=ide.1 \
		-rtc base=localtime \
		-device rtl8139,netdev=mynet0 -netdev user,id=mynet0 -device es1370

newhd:
	@qemu-img create -f qcow2 $(HDNAME).qcow2 $(HDSIZE)

