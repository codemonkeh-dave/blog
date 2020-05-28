# How to backup docker container volumes using powershell core

## Backup each directory into a Tar file

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
    # store list of directories in a variable
    $directories = Get-ChildItem -Directory

    # list commands to be run
    $directories | ForEach-Object { echo "tar -cvzf $($_.name).tgz $($_.name)" }

    # run commands listed above
    $directories | ForEach-Object { tar -cvzf "$($_.name).tgz" "$($_.name)" }

    ```

5. Now you are free to download or move the tar files to a backup location for safe keeping.

## Restore each Tar file back to their original directory

1. Login to the docker vm and elevate to root
2. Launch Powershell Core

```bash
pwsh
```

3. Open docker volumes directory

```bash
cd /var/lib/docker/volumes/
```
4. Copy/Move your backups (.tgz) files into the directory you want to restore them to.

```bash
cp \temp\*.tgz /var/lib/docker/volumes/
#note: replace \temp with the directory your backups are located in
```

5. Uncompress each file into their original directory

```bash
# store list of .tgz files in a variable
$files = Get-ChildItem -File -Filter *.tgz

# list commands to be run
$files | ForEach-Object { echo "tar -zxvf $($_.name)" }

# run commands listed above
$files | ForEach-Object { tar -zxvf "$($_.name)" }
```

6. Remove backups (IF NO LONGER NEEDED)

```bash
rm *.tgz
```