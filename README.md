A strange way to update your Debian-based system

sudo apt update && apt list --upgradable | awk '{print$1}' | cut -f1 -d '/' > some.txt && sed -i 1d some.txt && cat some.txt | xargs sudo apt install -y

We run 'sudo apt update' and after the command finishes, it says that, for example: 64 packages can be upgraded. Run 'apt list --upgradable' to see them.

We run 'apt list --upgradable' and shows some information about the packages.

Listing... Done 
ca-certificates/bionic-security,bionic-security,bionic-updates,bionic-updates 2021011918.04.2 all [upgradable from: 2021011918.04.1] 
curl/bionic-security,bionic-updates 7.58.0-2ubuntu3.16 amd64 [upgradable from: 7.58.0-2ubuntu3.15] 
element-desktop/unknown 1.9.0 amd64 [upgradable from: 1.8.5]

AWK 
awk '{print$1}' - will show us 'ca-certificates/bionic-security,bionic-security,bionic-updates,bionic-updates'

CUT 
cut -f1 -d '/' - will remove everything after the mentioned char 'ca-certificates'

SED 
sed -i 1d - will remove the first line in the text file which is 'Listing...'