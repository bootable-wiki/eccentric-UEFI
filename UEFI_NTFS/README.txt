Source: https://github.com/pbatard/rufus/blob/master/res/uefi/readme.txt
Modified on 2024 June 7th by https://github.com/CatherineDoyel

If you are on Windows & an administrator you should just use Rufus it will
handle the following automatically. However, if you are on a Mac, Linux or
other os follow along to create a Windows installer on that platform.

This directory contains the files of the FAT UEFI:NTFS partition added by
Rufus for NTFS and exFAT UEFI boot support.

These files can be placed any partition of disk other than the first.
It is hard coded to run EFI from the first partition formatted as either NTFS
or exFAT /efi/boot/bootXXXX.efi where XXXX is the CPU type (x86, arm, x64)

For example, how it could be used on 8 GB USB Disk.
First partition should be allocated from beginning of disk up to 7GB
        You can extract contents of the Windows ISO here.
Second partition 7GB to end of disk
        Must be FAT32, or FAT16 to comply with UEFI requirements.
        Copy these UEFI_NTFS files directly to this partition.

Example file Structure
NTFS 7GB partition
	When you open partition, you immediately see these files.
	They are directly placed on the root of the partition.
                boot            folder
                efi             folder
                sources         folder
                support         folder
                autorun.inf     file
                bootmgr         file
                bootmgr.efi     file
                setup.exe       file
FAT32 200MB partition
	When you open partition, you immediately see these files.
	They are directly placed on the root of the partition.
                EFI                     folder
                RUFUS_README.txt        file
                UEFI_NTFS_README.txt    file

See https://github.com/pbatard/uefi-ntfs for more details.

This folder contains the following data:

o Secure Boot signed NTFS UEFI drivers, derived from ntfs-3g [1].
  These drivers are the exact same as the read-only binaries from release 1.7,
  except for the addition of Microsoft's Secure Boot signature.
  Note that, per Microsoft's current Secure Boot signing policies, the 32-bit
  ARM driver (ntfs_arm.efi) is not Secure Boot signed.

o Non Secure Boot signed exFAT UEFI drivers from EfiFs [2].
  These drivers are the exact same as the binaries from EfiFs release 1.9 but,
  because they are licensed under GPLv3, cannot be Secure Boot signed.

o Secure Boot signed UEFI:NTFS bootloader binaries [3].
  These drivers are the exact same as the binaries from release 2.3, except for
  the addition of Microsoft's Secure Boot signature.
  Note that, per Microsoft's current Secure Boot signing policies, the 32-bit
  ARM bootloader (bootarm.efi) is not Secure Boot signed.

The above means that, if booting an NTFS partition on an x86_32, x86_64 or ARM64
system, Secure Boot does not need to be disabled.

This means that if you have to use exFAT then you need to disable secure boot.

[1] https://github.com/pbatard/ntfs-3g
[2] https://github.com/pbatard/efifs
[3] https://github.com/pbatard/uefi-ntfs
