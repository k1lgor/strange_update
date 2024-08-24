# A strange way to update your Debian-based system

`sudo apt update && apt list --upgradable 2>/dev/null | awk -F/ 'NR>1 {print $1}' | xargs -r sudo apt install -y`

1) We run `sudo apt update` and after the command finishes, it says that, for example: 64 packages can be upgraded.
2) After that run `apt list --upgradable` shows some information about the packages.

```bash
Listing... Done
ca-certificates/bionic-security,bionic-security,bionic-updates,bionic-updates 2021011918.04.2 all [upgradable from: 2021011918.04.1]
curl/bionic-security,bionic-updates 7.58.0-2ubuntu3.16 amd64 [upgradable from: 7.58.0-2ubuntu3.15]
element-desktop/unknown 1.9.0 amd64 [upgradable from: 1.8.5]
```

## `sudo apt update`

It fetches the latest information about available packages from the configured package repositories. Running this command ensures that you are working with the most current package data.

## `apt list --upgradable 2>/dev/null`

`apt list --upgradable` returns a list of installed packages that have newer versions available. The `2>/dev/null` part redirects any error messages (file descriptor 2) to `/dev/null`, effectively suppressing them, which can be useful to avoid cluttering the output with warnings or errors.

## `awk -F/ 'NR>1 {print $1}'`

`-F/`: Specifies `/` as the field separator.
`NR>1`: Skips the first line (header) by only processing lines where the line number (`NR`) is greater than 1.
`{print $1}`: Prints the first field (the package name) of each line. This extracts just the package names from the list of upgradable packages.

## `xargs -r sudo apt install -y`

`xargs`: Takes the package names output by `awk` and passes them as arguments to `sudo apt install -y`.
`-r`: Ensures `xargs` only runs the `apt install` command if there are package names to process (i.e., if the list is not empty).
`sudo apt install -y`: Installs the packages without prompting for confirmation (`-y`), using `sudo` to ensure the command has the necessary privileges.
