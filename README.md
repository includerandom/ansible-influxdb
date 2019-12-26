ansible-influxdb
=========

Install InfluxDB on a host


Requirements
------------

No special requirements.

Role Variables
--------------

### `vars`
influxdb_url: URL of source package for InfluxDB. Set in `vars`


### `defaults`

| Variable  | Default | Description |
| ---  | --- | --- |
|influxdb_version| 1.7.9| | 
|influxdb_index_version| tsi1| | 
|influxdb_meta_dir| /var/lib/influxdb/meta| | 
|influxdb_meta_retention_autocreate| true| | 
|influxdb_meta_logging_enabled| true| | 
|influxdb_admin_user| admin|
|influxdb_data_dir| /var/lib/influxdb/data | The directory where the TSM storage engine stores TSM files.|
|influxdb_data_wal_dir| /var/lib/influxdb/wal | The directory where the TSM storage engine stores WAL files.|
|influxdb_data_wal_fsync_delay| 0s | Values in the range of 0-100ms are recommended for non-SSD disks.|
|influxdb_data_index_version| inmem | The type of shard index to use for new shards.  The default is an in-memory index that is recreated at startup.  A value of "tsi1" will use a disk based index that supports higher cardinality datasets.|
|influxdb_data_trace_logging_enabled| false | Trace logging provides more verbose output around the tsm engine. Turning this on can provide more useful output for debugging tsm engine issues.|
|influxdb_data_query_log_enabled| true | The type of shard index to use for new shards.  The default is an in-memory index that is recreated at startup.  A value of "tsi1" will use a disk based index that supports higher Whether queries should be logged before execution. Very useful for troubleshooting, but will log any sensitive data contained within a query.|
|influxdb_data_validate_keys| false | Validates incoming writes to ensure keys only have valid unicode characters.  This setting will incur a small overhead because every key must be checked.|
|influxdb_data_cache_max_memory_size| 1g | CacheMaxMemorySize is the maximum size a shard's cache can reach before it starts rejecting writes.  Valid size suffixes are k, m, or g (case insensitive, 1024 = 1k).  Values without a size suffix are in bytes.|
|influxdb_data_cache_snapshot_memory_size| 25m | CacheSnapshotMemorySize is the size at which the engine will snapshot the cache and write it to a TSM file, freeing up memory Valid size suffixes are k, m, or g (case insensitive, 1024 = 1k).  Values without a size suffix are in bytes.|
|influxdb_data_cache_snapshot_write_cold_duration| 10m | CacheSnapshotWriteColdDuration is the length of time at which the engine will snapshot the cache and write it to a new TSM file if the shard hasn't received writes or deletes|
|influxdb_data_compact_full_write_cold_duration| 4h | CompactFullWriteColdDuration is the duration at which the engine will compact all TSM files in a shard if it hasn't received a write or delete|
|influxdb_data_max_concurrent_compactions| 0 | The maximum number of concurrent full and level compactions that can run at one time.  A value of 0 results in 50% of runtime.GOMAXPROCS(0) used at runtime.  Any number greater than 0 limits compactions to that value.  This setting does not apply to cache snapshotting.|
|influxdb_data_compact_throughput| 48m | CompactThroughput is the rate limit in bytes per second that we will allow TSM compactions to write to disk. Note that short bursts are allowed to happen at a possibly larger value, set by CompactThroughputBurst|
|influxdb_data_compact_throughput_burst| 48m | CompactThroughputBurst is the rate limit in bytes per second that we will allow TSM compactions to write to disk.|
|influxdb_data_tsm_use_madv_willneed| false | If true, then the mmap advise value MADV_WILLNEED will be provided to the kernel with respect to TSM files. This setting has been found to be problematic on some kernels, and defaults to off.  It might help users who have slow disks in some cases.|
|influxdb_data_max_series_per_database| 1000000 | The maximum series allowed per database before writes are dropped.  This limit can prevent high cardinality issues at the database level.  This limit can be disabled by setting it to 0.|
|influxdb_data_max_values_per_tag| 100000 | The maximum number of tag values per tag that are allowed before writes are dropped.  This limit can prevent high cardinality tag values from being written to a measurement.  This limit can be disabled by setting it to 0.|
|influxdb_data_max_index_log_file_size| 1m | The threshold, in bytes, when an index write-ahead log file will compact into an index file. Lower sizes will cause log files to be compacted more quickly and result in lower heap usage at the expense of write throughput.  Higher sizes will be compacted less frequently, store more series in-memory, and provide higher write throughput.  Valid size suffixes are k, m, or g (case insensitive, 1024 = 1k).  Values without a size suffix are in bytes.|
|influxdb_data_series_id_set_cache_size| 100 | The size of the internal cache used in the TSI index to store previously calculated series results. Cached results will be returned quickly from the cache rather than needing to be recalculated when a subsequent query with a matching tag key/value predicate is executed. Setting this value to 0 will disable the cache, which may lead to query performance issues.  This value should only be increased if it is known that the set of regularly used tag key/value predicates across all measurements for a database is larger than 100. An increase in cache size may lead to an increase in heap usage.|
|influxdb_coordinator_write_timeout| 10s | The default time a write request will wait until a "timeout" error is returned to the caller.|
|influxdb_coordinator_max_concurrent_queries| 0 | The maximum number of concurrent queries allowed to be executing at one time.  If a query is executed and exceeds this limit, an error is returned to the caller.  This limit can be disabled by setting it to 0.|
|influxdb_coordinator_query_timeout| 0s | The maximum time a query will is allowed to execute before being killed by the system.  This limit can help prevent run away queries.  Setting the value to 0 disables the limit.|
|influxdb_coordinator_log_queries_after| 0s | The time threshold when a query will be logged as a slow query.  This limit can be set to help discover slow or resource intensive queries.  Setting the value to 0 disables the slow query logging.|
|influxdb_coordinator_max_select_point| 0 | The maximum number of points a SELECT can process.  A value of 0 will make the maximum point count unlimited.  This will only be checked every second so queries will not be aborted immediately when hitting the limit.|
|influxdb_coordinator_max_select_series| 0 | The maximum number of series a SELECT can run.  A value of 0 will make the maximum series count unlimited.|
|influxdb_coordinator_max_select_buckets| 0 | The maximum number of group by time bucket a SELECT can create.  A value of zero will max the maximum number of buckets unlimited.|
|influxdb_retention_enabled| true | Determines whether retention policy enforcement enabled.|
|influxdb_retention_check_interval| 30m | The interval of time when retention policy enforcement checks run.|
|influxdb_shard_precreation_enabled| true | Determines whether shard pre-creation service is enabled.|
|influxdb_shard_precreation_check_interval| 10m | The interval of time when the check to pre-create new shards runs.|
|influxdb_shard_precreation_advance_period| 30m | The default period ahead of the endtime of a shard group that its successor group is created.|
|influxdb_monitor_store_enabled| true | Whether to record statistics internally.|
|influxdb_monitor_store_database| _internal | The destination database for recorded statistics|
|influxdb_monitor_store_interval| 10s | The interval at which to record statistics|
|influxdb_http_enabled| true | Determines whether HTTP endpoint is enabled.|
|influxdb_http_flux_enabled| false | Determines whether the Flux query endpoint is enabled.|
|influxdb_http_flux_log_enabled| false | Determines whether the Flux query logging is enabled.|
|influxdb_http_bind_address| ":8086" | The bind address used by the HTTP service.|
|influxdb_http_auth_enabled| false | Determines whether user authentication is enabled over HTTP/HTTPS.|
|influxdb_admin_user_name| admin| | 
|admin_user_password| "{{ influxdb_admin_user_password }}"| | 
|influxdb_http_realm| InfluxDB | The default realm sent back when issuing a basic auth challenge.|
|influxdb_http_log_enabled| true | Determines whether HTTP request logging is enabled.|
|influxdb_http_suppress_write_log| false | Determines whether the HTTP write request logs should be suppressed when the log is enabled.|
|influxdb_http_access_log_path| "" | When HTTP request logging is enabled, this option specifies the path where log entries should be written. If unspecified, the default is to write to stderr, which intermingles HTTP logs with internal InfluxDB logging.  If influxd is unable to access the specified path, it will log an error and fall back to writing the request log to stderr.|
|influxdb_http_access_log_status_filters| [] | Filters which requests should be logged. Each filter is of the pattern NNN, NNX, or NXX where N is a number and X is a wildcard for any number. To filter all 5xx responses, use the string 5xx.  If multiple filters are used, then only one has to match. The default is to have no filters which will cause every request to be printed.|
|influxdb_http_write_tracing| false | Determines whether detailed write logging is enabled.|
|influxdb_http_pprof_enabled| true | Determines whether the pprof endpoint is enabled.  This endpoint is used for troubleshooting and monitoring.|
|influxdb_http_pprof_auth_enabled| influxdb_http_pprof_enabled | Enables authentication on pprof endpoints. Users will need admin permissions to access the pprof endpoints when this setting is enabled. This setting has no effect if either auth-enabled or pprof-enabled are set to false.|
|influxdb_http_debug_pprof_enabled| false | Enables a pprof endpoint that binds to localhost:6060 immediately on startup.  This is only needed to debug startup issues.|
|influxdb_http_ping_auth_enabled| influxdb_http_pprof_enabled  | Enables authentication on the /ping, /metrics, and deprecated /status endpoints. This setting has no effect if auth-enabled is set to false.|
|influxdb_http_https_enabled| false | Determines whether HTTPS is enabled.|
|influxdb_http_https_certificate| /etc/ssl/influxdb.pem | The SSL certificate to use when HTTPS is enabled.|
|influxdb_http_https_private_key| "" | Use a separate private key location.|
|influxdb_http_shared_secret| "" | The JWT auth shared secret to validate requests using JSON web tokens.|
|influxdb_http_max_row_limit| 0 | The default chunk size for result sets that should be chunked.|
|influxdb_http_max_connection_limit| 0 | The maximum number of HTTP connections that may be open at once.  New connections that would exceed this limit are dropped.  Setting this value to 0 disables the limit.|
|influxdb_http_unix_socket_enabled| false | Enable http service over unix domain socket|
|influxdb_http_bind_socket| /var/run/influxdb.sock | The path of the unix domain socket.|
|influxdb_http_max_body_size| 25000000 | The maximum size of a client request body, in bytes. Setting this value to 0 disables the limit.|
|influxdb_http_max_concurrent_write_limit| 0 | The maximum number of writes processed concurrently.  Setting this to 0 disables the limit.|
|influxdb_http_max_enqueued_write_limit| 0 | The maximum number of writes queued for processing.  Setting this to 0 disables the limit.|
|influxdb_http_enqueued_write_timeout| 0 | The maximum duration for a write to wait in the queue to be processed.  Setting this to 0 or setting max-concurrent-write-limit to 0 disables the limit.|
|influxdb_logging_format| auto | Determines which log encoder to use for logs. Available options are auto, logfmt, and json. auto will use a more a more user-friendly output format if the output terminal is a TTY, but the format is not as easily machine-readable. When the output is a non-TTY, auto will use logfmt.|
|influxdb_logging_level| info | Determines which level of logs will be emitted. The available levels are error, warn, info, and debug. Logs that are equal to or above the specified level will be emitted.|
|influxdb_logging_suppress_logo| false | Suppresses the logo output that is printed when the program is started.  The logo is always suppressed if STDOUT is not a TTY.|
|influxdb_subscriber_enabled| true | Determines whether the subscriber service is enabled.|
|influxdb_subscriber_http_timeout| 30s | The default timeout for HTTP writes to subscribers.|
|influxdb_subscriber_insecure_skip_verify| false | Allows insecure HTTPS connections to subscribers.  This is useful when testing with self-signed certificates.|
|influxdb_subscriber_ca_certs| "" | The path to the PEM encoded CA certs file. If the empty string, the default system certs will be used|
|influxdb_subscriber_write_concurrency| 40 | The number of writer goroutines processing the write channel.|
|influxdb_subscriber_write_buffer_size| 1000 | The number of in-flight writes buffered in the write channel.|
|influxdb_graphite_enabled| false | Determines whether the graphite endpoint is enabled.|
|influxdb_graphite_database| graphite| | 
|influxdb_graphite_retention_policy| ""| | 
|influxdb_graphite_bind_address| ":2003"| | 
|influxdb_graphite_protocol| tcp| | 
|influxdb_graphite_consistency_level| one| | 
|influxdb_graphite_batch_size| 5000 | Flush if this many points get buffered|
|influxdb_graphite_batch_pending| 10 | number of batches that may be pending in memory|
|influxdb_graphite_batch_timeout| 1s | Flush at least this often even if we haven't hit buffer limit|
|influxdb_graphite_tags|  "region=us-east" "zone=1c" | UDP Read buffer size, 0 means OS default. UDP listener will fail if set above OS max.  influxdb_graphite_udp_read_buffer| 0 This string joins multiple matching 'measurement' values providing more control over the final measurement name.  luxdb_graphite_separator| "." Default tags that will be added to all metrics.  These can be overridden at the template level or by tags extracted from metric|
|influxdb_graphite_templates| "*.app env.service.resource.measurement" "server.*" | Each template line requires a template pattern.  It can have an optional filter before the template and separated by spaces.  It can also have optional extra tags following the template.  Multiple tags should be separated by commas and no spaces similar to the line protocol format.  There can be only one default template.|
|influxdb_collectd_enabled| false| | 
|influxdb_collectd_bind_address| ":25826"| | 
|influxdb_collectd_database| collectd| | 
|influxdb_collectd_retention_policy| ""| | 
|influxdb_collectd_typesdb| /usr/local/share/collectd| | 
|influxdb_collectd_security_level| none| | 
|influxdb_collectd_auth_file| /etc/collectd/auth_file| | 
|influxdb_collectd_batch_size| 5000 | Flush if this many points get buffered|
|influxdb_collectd_batch_pending| 10 | Number of batches that may be pending in memory|
|influxdb_collectd_batch_timeout| 10s | Flush at least this often even if we haven't hit buffer limit|
|influxdb_collectd_read_buffer| 0 | UDP Read buffer size, 0 means OS default. UDP listener will fail if set above OS max.|
|influxdb_collectd_parse_multivalue_plugin| split | "split" is the default behavior for backward compatibility with previous versions of influxdb.|
|influxdb_opentsdb_enabled| false| | 
|influxdb_opentsdb_bind_address| ":4242"| | 
|influxdb_opentsdb_database| opentsdb| | 
|influxdb_opentsdb_retention_policy| ""| | 
|influxdb_opentsdb_consistency_level| one| | 
|influxdb_opentsdb_tls_enabled| false| | 
|influxdb_opentsdb_certificate| /etc/ssl/influxdb.pem| | 
|influxdb_opentsdb_log_point_errors| true| | 
|influxdb_opentsdb_batch_size| 1000 | Flush if this many points get buffered|
|influxdb_opentsdb_batch_pending| 5 | Number of batches that may be pending in memory|
|influxdb_opentsdb_batch_timeout| 1s | Flush at least this often even if we haven't hit buffer limit|
|influxdb_udp_enabled| false ||
|influxdb_udp_bind_address| ":8089" ||
|influxdb_udp_database| udp ||
|influxdb_udp_retention_policy| "" ||
|influxdb_udp_precision| "" | InfluxDB precision for timestamps on received points ("" or "n", "u", "ms", "s", "m", "h")|
|influxdb_udp_batch_size| 5000 | Flush if this many points get buffered|
|influxdb_udp_batch_pending| 10 | Number of batches that may be pending in memory|
|influxdb_udp_batch_timeout| 1s | Will flush at least this often even if we haven't hit buffer limit|
|influxdb_udp_read_buffer| 0 | UDP Read buffer size, 0 means OS default. UDP listener will fail if set above OS max.|
|influxdb_continuous_queries_enabled| true | Determines whether the continuous query service is enabled.|
|influxdb_continuous_queries_log_enabled| true | Controls whether queries are logged when executed by the CQ service.|
|influxdb_continuous_queries_query_stats_enabled| false | Controls whether queries are logged to the self-monitoring data store.|
|influxdb_continuous_queries_run_interval| 1s | interval for how often continuous queries will be checked if they need to run |
|influxdb_tls_ciphers | TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305 TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 | Determines the available set of cipher suites. See https://golang.org/pkg/crypto/tls/#pkg-constants for a list of available ciphers, which depends on the version of Go (use the query SHOW DIAGNOSTICS to see the version of Go used to build InfluxDB). If not specified, uses the default settings from Go's crypto/tls package.|
|influxdb_tls_min_version| tls1.2 | Minimum version of the tls protocol that will be negotiated. If not specified, uses the default settings from Go's crypto/tls package.|
|influxdb_tls_max_version| tls1.2 | Maximum version of the tls protocol that will be negotiated. If not specified, uses the default settings from Go's crypto/tls package.|

Dependencies
------------

No external dependencies

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: heytrav.influxdb, influxdb_admin_user_password: "{{ vault_admin_user_password }}" }

License
-------

BSD

Author Information
------------------

travis@catalyst
