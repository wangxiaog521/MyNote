## rman configure
```sql
-- check all the info
show all

-- configure parallel
CONFIGURE DEVICE TYPE DISK PARALLELISM 1

-- 
BACKUP AS COMPRESSED BACKUPSET INCREMENTAL FROM SCN 112616279941 FILESPERSET 1 DATABASE FORMAT '/data1/arch/backup/increem14/ora10_scn_%U' TAG 'SW';
```

col min_scn for 999999999999999  
select min(checkpoint_change#) min_scn from v$datafile_header;