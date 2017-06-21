# telegraf-execnfsiostat
Simple nfsiostat collector script for the Telegraf exec input
## Configuration
Sample telegraf configuration file, place in /etc/telegraf/telegraf.d/nfsiostat.conf

```
[[inputs.exec]]
  # Shell/commands array
  # compatible with old version
  # we can still use the old command configuration
  # command = "/usr/bin/line_protocol_collector"
  commands = ["/usr/local/bin/influx_nfsiostat"]
  ## Timeout for each command to complete.
  timeout = "5s"
  # Data format to consume.
  # NOTE json only reads numerical measurements, strings and booleans are ignored.
  data_format = "influx"
```
## Measurements & Fields:
The following fields are collected as floats under the execnfsiostat measurement. Descriptions per the manpage:
..* avg_rtt - This is the duration from the time that client's kernel sends the RPC request until the time it receives the reply.
..* avg_exe - This is the duration from the time that NFS client does the RPC request to its kernel until the RPC request is completed, this includes the RTT time above.
..* kbop - This is the number of kB written/read per each operation.
..* kbs - This is the number of kB written/read per second.
..* ops_sec - This is the number of operations per second.
..* retrans - This is the number of retransmissions.
..* rpc_bklog - This is the length of the backlog queue.
## Tags:
The measurements have the following tags:
..* host - the host where data was collected
..* mount - the filesystem mountpoint
..* option - either none (2-sec average) or all (average since mount)
..* type - one of {read,write,general}
