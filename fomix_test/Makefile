BUILD:=./build

HD_IMG_NAME := "fomo.img"

all: ${BUILD}/boot/boot.o
	-@del /F /Q $(HD_IMG_NAME)
	-@bximage -q -hd=26 -func=create -sectsize=512 -imgmode=flat $(HD_IMG_NAME)
	dd if=$(BUILD)/boot/boot.o of=$(HD_IMG_NAME) bs=512 seek=0 count=1 conv=notrunc

${BUILD}/boot/%.o: boot/%.asm
	-@mkdir ${BUILD}/boot
	nasm $< -o $@

clean:
	-@del /F /Q /S ${BUILD}

bochs: all
	bochs -q -f bochsrc

binbuild: boot/%.asm
	nasm $< -o {BUILD}/boot/%.bin

qemu:
	-@qemu-system-x86_64 -hda $(HD_IMG_NAME)