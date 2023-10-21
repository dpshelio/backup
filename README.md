# backup

Small application to configure certain folders in the computer to be backed up on a cloud provider reachable via [rclone](https://rclone.org/).

## Plan

cli that could add directories to a config file, and sync them daily via a cron job (or similar).

For example,

```
~/Documents/ProjectX $ backup add . [remoteName]
```

Should add that ProjectX folder to a config file such that:

```
[[connection]]
folderNme: backup
remote: yourRemote
[[locations]]
- ~/Documents/ProjectX|yourRemote:backup/ProjectX
```

And create a folder remotely, under the config remote.

```
~/Documents/ProjectX $ backup status
 5 modified/new files since last update [x hours ago]
 1 new git repository
```

```
~/Documents/ProjectX $ backup list
 3 local folders are backed up:
  - ProjectX
  - Marks
  - Music
```

Each top-level directory can have a `.backupignore` or (internally to a child directory - maybe)


```
~/Documents/ProjectX $ backup sync [folder]
```

Could be used to run sync when needed.

```
~/Documents/ProjectX $ backup config
```

Could be interactive or manually to add everything needed (remote, folder name, ...)


## Why?

I want a system that I can keep the folder structure as I like, and only sync
what's needed on a remote system. Git repositories shouldn't be include but the
tool should commit and push local changes to a fork/branch. 


## some possible useful links

- [backup-ing with cron+rclone](https://contabo.com/blog/linux-server-backup-using-rclone/)
- [miniBackup](https://github.com/Johannes11833/MiniAutoBackup/blob/main/src/main.py) a backup program for one folder via docker
- [rclone helper](https://github.com/sourabh945/rclone_helper/blob/main/main.py) to backup programs.
- [No syncing repositories](https://forum.rclone.org/t/ignore-all-git-repos-when-syncing/33023/5) - though the solution is `find`ing them first.

## commands

- `rclone mkdir ext:folder` creates that folder there!
- `rclone sync Forder1 ext:backup/` Doesn't create Folder1 under backup, but the content of it. However, `rclone sync Folder1 ext:backup/Folder1` works.

