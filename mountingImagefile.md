|Command|output|Commnets|
|--|--|--|
|find . -type f -exec basename {} \ |name of each files in a directory||
|basename |basename removes directory path and returns the file name||
|dconf-editor |use to disable auto mount of a external drive on linux||
|sudo dc3dd if=/dev/sdb of=image.img |to create an image file of usb drive||
|du -h image.img|to check the size in human readble format|output m will represent mb|
|sudo md5sum /dev/sdb > device.txt|to create md5sum hash of a file||
|diff -c file1 file2 |to compare file and show the difference||


## Steps to mount a dd image file on linux/unix using command line

1. create mount point `sudo mkdir /mnt/image`
2. `fdisk -l lab4-practice/image.img` to check the offset<br>
output: <br>
Disk lab4-practice/image.img: 961 MiB, 1007681536 bytes, 1968128 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x003bc360

Device                   Boot Start     End Sectors  Size Id Type
lab4-practice/image.img1 *       32 1968127 1968096  961M  6 FAT16

3. from the above output, we can observe that block-size is 512 bytes and the start-block is 32. The offset is 512 * 128 = 65536/we can use inbult calculation
So the mount command would be:<br>
`sudo mount -t auto -o loop,offset=$((32*512)) lab4-practice/image.img /mnt/image`

### Tried below commnds without sudo
`mount -t auto -o loop lab4-practice/image.img /mnt/image` 


#### How to check if mounted image is read only
pending






