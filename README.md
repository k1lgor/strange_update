## A strange way to update your Debian-based system

`sudo apt update && apt list --upgradable | awk '{print$1}' | cut -f1 -d '/' > some.txt && sed -i 1d some.txt && cat some.txt | xargs sudo apt install -y`

1) We run `sudo apt update` and after the command finishes, it says that, for example: 64 packages can be upgraded. 
2) After that run `apt list --upgradable` shows some information about the packages.

```
Listing... Done 
ca-certificates/bionic-security,bionic-security,bionic-updates,bionic-updates 2021011918.04.2 all [upgradable from: 2021011918.04.1] 
curl/bionic-security,bionic-updates 7.58.0-2ubuntu3.16 amd64 [upgradable from: 7.58.0-2ubuntu3.15] 
element-desktop/unknown 1.9.0 amd64 [upgradable from: 1.8.5]
```
### AWK 
`awk '{print$1}'`
* will show us the first argument `ca-certificates/bionic-security,bionic-security,bionic-updates,bionic-updates`

### CUT 
`cut -f1 -d '/'`
* `cut` - remove sections from each line of files
* `-f1` - select only these fields;  also print any line that contains no delimiter character, unless the -s option is specified
* `-d '/'` - use DELIM instead of TAB for field delimiter

`ca-certificates/bionic-security,bionic-security,bionic-updates,bionic-updates` ==> `ca-certificates`

### SED 
`sed -i 1d`
* will remove the first line in the text file `Listing...`
* `sed` - stream editor for filtering and transforming text
* `-i 1d` - edit files in place (makes backup if extension supplied)

### CAT
`cat some.txt`
* `cat` - concatenate files and print on the standard output

### XARGS
`xargs sudo apt install -y`
* `xargs` - build and execute command lines from standard input
