# Oracle
To get database size

select sum(bytes / (1024*1024)) "DB Size in MB" from dba_data_files; 
