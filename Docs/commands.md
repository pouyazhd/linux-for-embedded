# Basic commands

## Topics

1. ls
   1. -atlash
   2. link direcrories
   3. lsusb
   4. lsblk
   5. lspci
2. tree
3. cd
4. rm
5. mv
6. mkdir
7. cp
8. dd
9. tar
10. top
11. grep
12. echo
13. free
14. df
15. du
16. chmod
17. mount
18. forbidden commands

## ls

list the files, directories and etc.

```bash
ls [flags] [Path]
```

**flags**:

* l: shows the list
* a: show all (include hidden files/directories)
* s: show the size
* h: human readable
* s: sort the output
* t: sort based on time

### lsblk

shows the storage blocks

### lsusb

shows the usb devices connected

### lspci

shows the PCI devices

## Tree

Show the directories files

```bash
tree [flags] [path]
```

## cd

change directory

```bash
cd [Path]
```

## rm

remove files and directories

```bash
rm [flags] [files and direcories]
```

**flags**:

* r: recursivly
* f: force
* i: ask before delete every file
* v: verbosely delete
* d: delete directory

## mv

Move files and directoies

```bash
mv [flags] [sources] [destination]
```

**flags**:

* f: forcefully move
* i: ask before move every file
* v: verbosely move files
* u: update destination( move only if the newer version of files)

## cp

Copy files

```bash
cp [flags] [sources] [detination]
```

**flags**:

* r: recursivly
* f: overwrite to destination
* n: do not overwrite
* s: make symbolic links instead of copying

## mkdir

make directory( or directories)

```bash
mkdir [flags] [list of directories]
```

**flags**:

* p: parent
* v: verbose
* m: mode

## tar

Convert files into a one file.

> use for backup files and directories

```bash
tar [flags] [tar-file-name] [list of files and directories]
```

**flags**:

* c: compress
* z: zip (use gzip)
* v: verbose
* f: file
* x: extract

**to compress a file using tar**:

```bash
tar -czvf [tar-file-name.tar.gz(.tgz)] [list of files and directories]
```

**To extract file using tar**:

```bash
tar -xzvf [tar-file-name.tar.gz(.tgz)] [destination]
```

## dd

Data disk. Use for creating file or space

```bash
dd [flags]
```

**flags**:

* if: path to input file
* of: path to output file
* bs: block size
* count: number of repating

```bash
# EXAMPLE1: create a file with 1Gbyte size at /tmp directory filled with zero
dd if=/dev/zero of=/tmp/myfile bs=1M count=1024

# EXAMPLE2: backup a directory of a disk and archive it
dd if=/etc/ | gzip -c /tmp/etc.backup
```

## top

shows the list of processes, IOs, CPU usage, RAM usage and etc

## grep

filter output of commands based on patterns

```bash
grep [flags] [prompt]
```

**flags**:

* A: shows the next lines based on number after this flag
* v: cases does not match with pattern

## xargs

## find

## awk

## free

## echo

## df

## du

## chmod

## mount

## shutdown

shutdown, reboot the system

```bash
shutdown [flag] [time] [Message to other users work on the computer]
```

**flags**:

* r: reboot
* P: poweroff
* H: halt the system
* c: cancel the operation

**time**:

* now: shutdown right now
* +n: shutdown n munute later
* "hh:mm": shutdown at time hh:mm

```bash
# EXAMPLE: reboot the system at midnight
shutdown -r "00:00" "The system will be reboot at midnight."
```

## fobidden commands

**Clear everything**:

```bash
sudo rm -rf /*
```

**Move to null**:

```bash
mv [sources] /dev/null
```

**Write `zero`, `one` or `random` on entire a disk**:

```bash
# USE IT CAREFULLY
dd if=/dev/one of=/dev/sdx bs=2M
```
