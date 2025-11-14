- originated with `Windows NT` in 1993 - developed by Microsoft
- Many `more features` than FAT
- greater `reliability, security and support` for large devices
- **Everything is a file** (unlike FAT)
- NTFS is based around the `Master File Table (MFT)` concept
- the MFT contains information about all files and directories on the volume
---
***NTFS Files***  
0. `$MFT` - master file table
1. `$MftMirr` - master file table mirror - copy of first part of $MFT
2. `$Logfile` - complex file logging disk operations
3. `$Volume` - information about the volume
4. `$AttrDef` - attribute definitions for every file on the volume
5. `"."` - the root folder
6. `$Bitmap` - cluster bitmap - shows used clusters, 1 bit per cluster
7. `$Boot` - boot data located at the beginning of partition (volume boot record)
8. `$BadClus` - points to bad clusters on the volume
9. `$Secure` - secure descriptors for all files on the volume
10. `$Upcase` - table of Unicode characters used for sorting filenames
11. `$Extend` - folder containing files of metadata
All of these files are located  within the `[root]` folder within FTK Imager
---
***Master File Table (MFT)***
- information about individual files and directories is stored in what is known as an MFT entry or record
- each MFT entry is `1024 bytes in size` 
- the MFT (`filename $MFT`) has an MFT entry for itself - this is the first entry (entry 0)
- the partition boot sector `aka VBR` (sector 0) `points at $MFT` - its a file. It can be stored anywhere in the partition
- An MFT entry:
	- one entry for every single file and folder on the system
	- 1 entry = 1024 bytes ***ALWAYS*** 
	- it contains an MFT entry header, attributes and typically some unused space
	- each attribute has 2 parts:
		- `header` (24 or 64 bytes in length)
			- example of an attribute header - look at `Attribute Header Example`
			- first 4 bytes say the type identifier. different attribute types located at `Attribute Types Table` 
			- 
			- if the file is small and the whole of it can fit in the MFT we call this a `resident file` (file size  << 1024 bytes) 
			- if the file size is `greater than 1024 bytes` this is called a non-resident file
				- in this case, attribute headers point to the cluster(s) where the remaining data is stored
				- typically it is the `$DATA` attribute which is too large
				- when an attribute is split over clusters, the `runs are stored in the header of the attribute` which means the header of a non-resident attribute is longer than that of a resident attribute
					- an example of this would look like: 
						- `Start: 48 Len: 5`
						- `Start: 80 Len: 2`
						- `Start: 56 Len: 4`
		- `content` (variable length)
