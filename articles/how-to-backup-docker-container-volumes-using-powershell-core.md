# How to backup docker container volumes using powershell core

## Backup Steps

1. Login to the docker vm and elevate to root
2. Launch Powershell Core

```bash
pwsh
```
> If you don't have powershell core installed, see [Installing Powershell Core on Linux](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-7)

3. Open docker volumes directory

```bash
cd /var/lib/docker/volumes/
```

4. Compress each directory into a file with a corresponding name

```bash
# store list of directories in variable
$directories = Get-ChildItem
# list commands to be run
$directories | ForEach-Object { echo "tar -cvzf $($_.name).tgz $($_.name)" }
# run commands
$directories | ForEach-Object { tar -cvzf "$($_.name).tgz" "$($_.name)" }

```

5. Now you are free to download or move the tar files to a backup location for safe keeping.

## Restore Steps

> Coming soon