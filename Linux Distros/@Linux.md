## Some Helpful Commands

| Command                           | Description                                                 |
| --------------------------------- | ----------------------------------------------------------- |
| sudo chmod -R a+rw folder/        | Give read/write perms to all users for every file in folder |
| sudo reboot                       | Reboot                                                      |
| tail -f /var/log/messages         | listen to the system logs                                   |
| fuser -k 8080/tcp                 | kill process using port 8080                                |
| find . -name "foo*" 2>/dev/null   | Find files recursively with match foo\                      |
| chown -R someuser:somegroup *.pdf |                                                             |

## OS Information Commands
| Command           | Description          |
| ----------------- | -------------------- |
| cat /proc/cpuinfo | Show CPU information |
| uname -a          | Show OS Information  |

## File Hierarchy Standard (FHS)

| Path   | Content                             |
| ------ | ----------------------------------- |
| /bin   | Binaries (User)                     |
| /boot  | Static boot loader files            |
| /etc   | Host specific configs               |
| /lib   | Shared libraries and kernel modules |
| /sbin  | Binaries (System/root)              |
| /var   | Varying files (e.g. Logs)           |
| /usr   | 3rd party software                  |
| /proc  | Pseudo file system                  |
| /sys   | Pseudo file system                  |
| /mnt   | Mountpoint for internal drives      |
| /media | Mountpoint for external drives      |
| /home  | User homes                          |
| /run   | PID files of running processes      |
## Basic Commands

### File System Commands
|Command|Param|Description|
|---|---|---|
|`cd`|`-`|Navigate to last dir|
||`~`|Navigate to home|
||`~username`|Navigate to home of specified user|
|`pwd`||Print working dir|
|`ls`||Print dir content|
||`-l`|Format as list|
||`-a`|Show hidden items (`-A` without `.` and `..`)|
||`-r`|Invert order|
||`-R`|Recurse|
||`-S`|Sort by size|
||`-t`|Sort by date modified|
|`mkdir`|`-p`|Create dir with parents|
|`cp`|`-r`|Copy dir|
|`rmdir`|`-p`|Remove dir and empty parents|
|`rm`|`-rf`|Remove dir recursively, `-f` without confirmation|
|`mv`||Move recursively|
|`find`|`-iname pattern`|Search dir/file case-insensitive|
||`-mmin n`|Last modified n minutes ago|
||`-mtime n`|Last modified n days ago|
||`-regex pattern`|Path matches pattern|
||`-size n[kMG]`|By file size (`-n` less than; `+n` greater than)|
||`! searchparams`|Invert search|

### File Manipulation

|Command|Param|Description|
|---|---|---|
|`cat`|`file`|Print content|
|`tac`|`file`|Print content inverted|
|`sort`|`file`|Print sorted|
||`file -r -u`|Print sorted descending without dublicates|
|`wc`|`file`|Count Lines, Words, Chars (Bytes)|
|`head`|`-n10 file|tail -n5`|
|`tail`|`-f file`|Print new lines automatically|
|`cut`|`-f -4,7-10,12,15- file`|Print selected fields (tab delimited)|
||`-c -4,7-10,12,15- file`|Print selected characters positions|
||`-f 2,4 -d, --output-delimiter=$'\t' file`|Change delimiter (but use tab for output)|
|`uniq`|`file`|Hide consecutive identical lines|
||`file -c`|Show consecutive identical line count|
||`file -u`|Hide consecutive identical lines|
|`file`|`file`|Get file type
## Disk and File System Management

### General Disk Manipulation (non-LVM)

Creating physical partitions is **not required**! You can create PVs directly!

| Command                                     | Description                          |
| ------------------------------------------- | ------------------------------------ |
| `fdisk -l`                                  | List physical disks and partitions   |
| `fdisk /dev/sdb`  <br>`n`                   | Create new partition                 |
| `fdisk /dev/sdb`  <br>`t`  <br>`8e`         | Change partition type to _Linux LVM_ |
| `mkfs.xfs /dev/myVG/myVol`                  | Format LV with XFS                   |
| `mkfs.ext4 -f /dev/myVG/myVol`              | Format LV with EXT4 (overwrite)      |
| `blkid /dev/myVG/myVol`                     | Show UUID and formatting of volume   |
| `mount`                                     | Show what is mounted where           |
| `mount -t ext4 /dev/myVG/myVol /mountpoint` | Mount LV to /mountpoint              |
| `umount /dev/myVG/myVol`                    | Unmount LV from /mountpoint          |
| `umount /mountpoint`                        | Unmount LV from /mountpoint          |
| `mount -a`                                  | Mount as configured in /etc/fstab    |
| `df`                                        | Show disk usage                      |
| `xfs_growfs /dev/myVG/myVol`                | Resize xfs filesystem                |
| `resize2fs /dev/myVG/myVol`                 | Resize ext3/4 filesystem             |