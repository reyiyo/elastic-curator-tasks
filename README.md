This docker image runs curator tasks against an elasticsearch cluster to manage its indices.

The list of tasks currently are:

- **Optimize indices**: forceMerge `INDEX_PREFIX` prefixed indices older than `INDEX_ROTATION_TIME` `TIME_UNIT` (based on index `creation_date`) to 1 segments per shard. Delay 120 seconds between each forceMerge operation to allow the cluster to quiesce. Skip indices that have already been forcemerged to the minimum number of segments to avoid reprocessing.
- **Purge old indices**: Delete indices older than `$INDEX_MAX_AGE` `$TIME_UNIT` (based on index `creation_date`), for `$INDEX_PREFIX` prefixed indices. Ignore the error if the filter does not result in an actionable list of indices and exit cleanly.


## Configuration

- `ES_HOST`: The hostname or IP address of the elasticsearch cluster.
- `ES_PORT`: The port of the elasticsearch cluster.
- `ES_AUTH`: Any http auth string for the cluster (i.e. `user:password`).
- `INDEX_PREFIX`: Prefix of indices to optimize/purge.
- `INDEX_ROTATION_TIME`: Indices older than this time will be optimized.
- `INDEX_MAX_AGE`: The maximum age an index can be until it is deleted.
- `TIME_UNIT`: The time unit in which the two previos values are expresed (`days`, `hours`, etc.).