# StarRocks version 2.5

## 2.5.0 RC

Release date: December 15, 2022

### New Features

- Supports querying Merge On Read tables using [Hudi catalogs](../data_source/catalog/hudi_catalog.md) or [Hudi external tables](../data_source/External_table.md#hudi-external-table). [#6780](https://github.com/StarRocks/starrocks/pull/6780)
- Supports querying data of the STRUCT and MAP types using [Hive catalogs](../data_source/catalog/hive_catalog.md), Hudi catalogs, or [Iceberg catalogs](../data_source/catalog/iceberg_catalog.md). [#10677](https://github.com/StarRocks/starrocks/issues/10677)
- Provides [block cache](../data_source/Block_cache.md) to improve access performance of hot data stored in external storage systems, such as HDFS. [#11597](https://github.com/StarRocks/starrocks/pull/11579)
- [Preview] Supports creating [Delta Lake catalogs](../data_source/catalog/deltalake_catalog.md), which allow direct queries on data from Delta Lake. [#11972](https://github.com/StarRocks/starrocks/issues/11972)
- [Preview] Hive catalogs, Hudi catalogs, and Iceberg catalogs are compatible with AWS Glue. [#12249](https://github.com/StarRocks/starrocks/issues/12249)
- [Preview] Supports creating [file external tables](../data_source/file_external_table.md), which allow direct queries on the Parquet and ORC files from HDFS or object stores. [#13064](https://github.com/StarRocks/starrocks/pull/13064)
- Supports creating materialized views based on Hive catalogs, Hudi catalogs, Iceberg catalogs, and materialized views. For more information, see [Materialized view](../using_starrocks/Materialized_view.md). [#11116](https://github.com/StarRocks/starrocks/issues/11116) [#11873](https://github.com/StarRocks/starrocks/pull/11873)
- Supports conditional updates for tables that use the Primary Key model. For more information, see [Change data through loading](../loading/Load_to_Primary_Key_tables.md). [#12159](https://github.com/StarRocks/starrocks/pull/12159)
- Supports [Query Cache](../using_starrocks/query_cache.md) that helps improve QPS and reduces the average latency of highly concurrent, simple queries by saving the intermediate computation results of queries. [#9194](https://github.com/StarRocks/starrocks/pull/9194)
- Supports specifying the priority of running Broker Load jobs. For more information, see [BROKER LOAD](../sql-reference/sql-statements/data-manipulation/BROKER%20LOAD.md) [#11029](https://github.com/StarRocks/starrocks/pull/11029)
- [Preview] Supports specifying the number of replicas of StarRocks native tables that needs to be loaded with data. For more information, see [CREATE TABLE](../sql-reference/sql-statements/data-definition/CREATE%20TABLE.md). [#11253](https://github.com/StarRocks/starrocks/pull/11253)
- [Preview] Supports [query queues](../administration/query_queues.md). [#12594](https://github.com/StarRocks/starrocks/pull/12594)
- Supports isolating the compute resources occupied by data loading, thereby limiting the resource consumption for data loading tasks. For more information, see [Resource group](../administration/resource_group.md). [#12606](https://github.com/StarRocks/starrocks/pull/12606)
- [Preview] Supports specifying the following data compression algorithms for StarRocks native tables: LZ4, Zstd, Snappy, and Zlib. For more information, see [Data compression](../table_design/data_compression.md). [#10097](https://github.com/StarRocks/starrocks/pull/10097) [#12020](https://github.com/StarRocks/starrocks/pull/12020)
- Supports [user-defined variables](../reference/user_defined_variables.md). [#10011](https://github.com/StarRocks/starrocks/pull/10011)
- Supports the [lambda expression](../sql-reference/sql-functions/Lambda_expression.md) and the following higher-order functions: [array_map](../sql-reference/sql-functions/array-functions/array_map.md),  [array_filter](../sql-reference/sql-functions/array-functions/array_filter.md), [array_sum](../sql-reference/sql-functions/array-functions/array_sum.md), and [array_sortby](../sql-reference/sql-functions/array-functions/array_sortby.md). [#9461](https://github.com/StarRocks/starrocks/pull/9461) [#9806](https://github.com/StarRocks/starrocks/pull/9806) [#10323](https://github.com/StarRocks/starrocks/pull/10323) [#14034](https://github.com/StarRocks/starrocks/pull/14034)
- Provides the QUALIFY clause that filters the results of [window functions](../sql-reference/sql-functions/Window_function.md). [#13239](https://github.com/StarRocks/starrocks/pull/13239)
- Supports specifying the result returned by the uuid or uuid_numeric function as a default value of a column when you create a table. For more information, see [CREATE TABLE](../sql-reference/sql-statements/data-definition/CREATE%20TABLE.md). [#11155](https://github.com/StarRocks/starrocks/pull/11155)
- Supports the following functions: [map_size](../sql-reference/sql-functions/map-functions/map_size.md), [map_keys](../sql-reference/sql-functions/map-functions/map_keys.md), [map_values](../sql-reference/sql-functions/map-functions/map_values.md), [max_by](../sql-reference/sql-functions/aggregate-functions/max_by.md), [sub_bitmap](../sql-reference/sql-functions/bitmap-functions/sub_bitmap.md), [bitmap_to_base64](../sql-reference/sql-functions/bitmap-functions/bitmap_to_base64.md), [host_name](../sql-reference/sql-functions/utility-functions/host_name.md), and [date_slice](../sql-reference/sql-functions/date-time-functions/date_slice.md). [#11299](https://github.com/StarRocks/starrocks/pull/11299) [#11323](https://github.com/StarRocks/starrocks/pull/11323) [#12243](https://github.com/StarRocks/starrocks/pull/12243) [#11776](https://github.com/StarRocks/starrocks/pull/11776) [#12634](https://github.com/StarRocks/starrocks/pull/12634) [#14225](https://github.com/StarRocks/starrocks/pull/14225)

### Improvements

- Optimizes the access performance on metadata when you query external data using [Hive catalogs](../data_source/catalog/hive_catalog.md), [Hudi catalogs](../data_source/catalog/hudi_catalog.md), or [Iceberg catalogs](../data_source/catalog/iceberg_catalog.md). [#11349](https://github.com/StarRocks/starrocks/issues/11349)
- Supports querying data of the ARRAY type using [Elasticsearch external tables](../data_source/External_table.md#elasticsearch-external-table). [#9693](https://github.com/StarRocks/starrocks/pull/9693)
- Optimizes the following aspects of materialized views:
  - Multi-table async refresh materialized views support automatic and transparent query rewrite based on the SPJG-type materialized views. For more information, see [Materialized view](../using_starrocks/Materialized_view.md#about-async-refresh-mechanisms-for-materialized-views). [#13193](https://github.com/StarRocks/starrocks/issues/13193)
  - Multi-table async refresh materialized views support multiple async refresh mechanisms. For more information, see [Materialized view](../using_starrocks/Materialized_view.md#enable-query-rewrite-based-on-async-materialized-views). [#12712](https://github.com/StarRocks/starrocks/pull/12712) [#13171](https://github.com/StarRocks/starrocks/pull/13171) [#13229](https://github.com/StarRocks/starrocks/pull/13229) [#12926](https://github.com/StarRocks/starrocks/pull/12926)
  - The efficiency of refreshing materialized views. [#13167](https://github.com/StarRocks/starrocks/issues/13167)
- StarRocks automatically sets an appropriate number of tablets when you create a table. For more information, see [CREATE TABLE](../sql-reference/sql-statements/data-definition/CREATE%20TABLE.md). [#10614](https://github.com/StarRocks/starrocks/pull/10614)
- Optimizes the following aspects of data loading:
  - Optimizes data loading performance, which gains a one-fold increase.  [#10138](https://github.com/StarRocks/starrocks/pull/10138)
  - Broker Load and Spark Load no longer need to depend on brokers for data loading when only one HA system or Kerberos is configured. For more information, see [Load data from HDFS or cloud storage](../loading/BrokerLoad.md) and [Bulk load using Apache Spark™](../loading/SparkLoad.md). [#9049](https://github.com/starrocks/starrocks/pull/9049) [#9228](https://github.com/StarRocks/starrocks/pull/9228)
  - Optimizes the performance of Broker Load when you load data from a large number of small ORC files. [#11380](https://github.com/StarRocks/starrocks/pull/11380)
  - Reduces the memory usage when you load data into tables of the Primary Key Model.
- Optimizes the `information_schema` database and the `tables` and `columns` tables within. Adds a new table `table_config`. For more information, see [Information Schema](../administration/information_schema.md). [#10033](https://github.com/StarRocks/starrocks/pull/10033)
- Optimizes data backup and restore:
  - Supports backing up and restoring data from multiple tables in a database at a time. For more information, see [Backup and restore data](../administration/Backup_and_restore.md).  [#11619](https://github.com/StarRocks/starrocks/issues/11619)
  - Supports backing up and restoring data from Primary Key tables. For more information, see Backup and restore.  [#11885](https://github.com/StarRocks/starrocks/pull/11885)
- Optimizes the following functions:
  - Adds an optional parameter for the [time_slice](../sql-reference/sql-functions/date-time-functions/time_slice.md) function, which is used to determine whether the beginning or end of the time interval is returned. [#11216](https://github.com/StarRocks/starrocks/pull/11216)
  - Adds a new mode `INCREASE` for the [window_funnel](../sql-reference/sql-functions/aggregate-functions/window_funnel.md) function to avoid computing duplicate timestamps. [#10134](https://github.com/StarRocks/starrocks/pull/10134)
  - Supports specifying multiple arguments in the [unnest](../sql-reference/sql-functions/array-functions/unnest.md) function. [#12484](https://github.com/StarRocks/starrocks/pull/12484)
  - lead() and lag() functions support querying HLL and BITMAP data. For more information, see [Window function](../sql-reference/sql-functions/Window_function.md). [#12108](https://github.com/StarRocks/starrocks/pull/12108)
  - The following ARRAY functions support querying JSON data: [array_agg](../sql-reference/sql-functions/array-functions/array_agg.md), [array_sort](../sql-reference/sql-functions/array-functions/array_sort.md), [array_concat](../sql-reference/sql-functions/array-functions/array_concat.md), [array_slice](../sql-reference/sql-functions/array-functions/array_slice.md), and [reverse](../sql-reference/sql-functions/array-functions/reverse.md). [#13155](https://github.com/StarRocks/starrocks/pull/13155)

### Bug Fixes

The following bugs are fixed:

- The append_trailing_char_if_absent() function may return an incorrect result when the first argument is empty. [#13762](https://github.com/StarRocks/starrocks/pull/13762)
- After a table is restored using the RECOVER statement, the table does not exist. [#13921](https://github.com/StarRocks/starrocks/pull/13921)
- The result returned by the SHOW CREATE MATERIALIZED VIEW statement does not contain the database and catalog specified in the query statement when the materialized view was created. [#12833](https://github.com/StarRocks/starrocks/pull/12833)
- Jobs of schema changes in the `waiting_stable` state can not be canceled. [#12530](https://github.com/StarRocks/starrocks/pull/12530)
- Running the `SHOW PROC '/statistic';` command on a Leader FE and non-Leader FE returns different results. [#12491](https://github.com/StarRocks/starrocks/issues/12491)

### Behavior Change

- The default value of the `AWS_EC2_METADATA_DISABLED` parameter is changed to `False`, which means that the metadata of Amazon EC2 is obtained to access AWS resources by default.
- The session variable `is_report_success` is renamed to `enable_profile` and can be queried using the SHOW VARIABLES statement.