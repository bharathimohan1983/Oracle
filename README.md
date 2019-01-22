# Oracle
To get database size

Option 1:
select sum(bytes / (1024*1024)) "DB Size in MB" from dba_data_files; 

Option 2:
SELECT a.data_size + b.temp_size + c.redo_size + d.controlfile_size 
"total_size in GB" 
FROM (SELECT SUM (bytes) / 1024 / 1024/1024 data_size FROM dba_data_files) a, 
(SELECT NVL (SUM (bytes), 0) / 1024 / 1024/1024 temp_size 
FROM dba_temp_files) b, 
(SELECT SUM (bytes) / 1024 / 1024/1024 redo_size FROM sys.v_$log) c, 
(SELECT SUM (BLOCK_SIZE * FILE_SIZE_BLKS) / 1024 / 1024/1024 
controlfile_size 
FROM v$controlfile) d;


