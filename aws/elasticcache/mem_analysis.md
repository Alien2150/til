What's bloating up my memory? 

1. Create a Elasticcache Snapshot
2. Export the Snapshot as described here: https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/backups-exporting.html
3. Download the rdb-file
4. Install this tool: https://github.com/sripathikrishnan/redis-rdb-tools
5. Run memory analysis for a specific db: ```rdb -c memory ~/Downloads/dump.rdb -n X -f memory.1.csv``` (Where X is the database)
6. Ramp up sqllite 
7. Create table: ```create table redis_metrics (
    database varchar not null,
    type varchar not null,
    key varchar not null,
    size_in_bytes int not null,
    encoding varchar not null,
    num_elements int not null,
    len_largest_element int not null,
    expiry timestamp
);```
8. Import the csv into sql-lite
9. Run analysis on SQL :-)
