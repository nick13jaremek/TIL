# Problem

Files are usually downloaded from the Internet in a compressed format to reduce traffic overhead. In order to deal with such files, a decompression tool or utility is required.

# Solution

Several alternatives exist to decompress a file. 

1. By using the OS GUI windows and such, go the folder containing the compressed file, right-click on it, and select the *Extract here* (or similar option).

2. By using a CLI tool known as *gunzip*, you can extract the contents of the compresed file. Consider a compressed SQL file *sample.sql.gz*. In order to extract it you may run the following command:
`gunzip sample.sql.gz`

3. Files compressed using Gzip or Gunzip yield *.gz* formats. In order to decompress this kind of files using the *tar* CLI tool, one needs to run the following command:
`tar -zxvf sample.sql.gz`

The flags indicate the following:
- *z*: filter the archive through *gzip*. This option tells tar to read or write archives through gzip, allowing tar to directly operate on several kinds of compressed archives transparently.
- *x*: extract files from archive.
- *v*: verbose mode activated. Show the files being worked on as tar is running.
- *f*: this option determines the name of the archive file that tar will work on. If you don't specify this argument, then tar will examine the environment variable TAPE. If it is set, its value will be used as the archive name. Otherwise, tar will use the default archive, determined at compile time.
