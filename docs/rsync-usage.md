# RSYNC: Usage

## Sync from source to destination

```bash
rsync -av --delete /path/to/source/ /path/to/destination/

# command can be run in dry-run mode to see what changes will happen
rsync -av --delete --dry-run /path/to/source/ /path/to/destination/
```
