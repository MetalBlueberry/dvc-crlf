# DVC CRLF issue

```txt
DVC version: 1.7.2 (pip)
---------------------------------
Platform: Python 3.6.9 on Linux-5.3.0-28-generic-x86_64-with-Ubuntu-18.04-bionic
Supports: All remotes
Cache types: hardlink, symlink
Cache directory: ext4 on /dev/nvme0n1p5
Workspace directory: ext4 on /dev/nvme0n1p5
Repo: dvc, git
```

> Cache is committed to the repo so it can be viewed

## Reproduce

- init git and dvc
- create a script.sh with CRLF line endings
- dvc add script.sh
- change CRLF ending to LF
- try to add it again, (doesn't detect changes)

## Obtained

script.sh is stored with CRLF in cache, so when you run `dvc checkout` it always comes back to CRLF line endings even if you modify it locally.

## Expected

script.sh should keep the original CRLF line endings or at least store the cache content always with LF endings.

## Consequences

- CRLF and LF cannot be modified after first commit
- md5 file name doesn't match the file content hash
