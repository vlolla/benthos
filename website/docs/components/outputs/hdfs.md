---
title: hdfs
type: output
status: stable
categories: ["Services"]
---

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the contents of:
     lib/output/hdfs.go
-->

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


Sends message parts as files to a HDFS directory.

```yaml
# Config fields, showing default values
output:
  hdfs:
    hosts:
      - localhost:9000
    user: benthos_hdfs
    directory: ""
    path: ${!count("files")}-${!timestamp_unix_nano()}.txt
    max_in_flight: 1
```

Each file is written with the path specified with the 'path' field, in order to
have a different path for each object you should use function interpolations
described [here](/docs/configuration/interpolation#bloblang-queries). When sending
batched messages the interpolations are performed per message part.

## Performance

This output benefits from sending multiple messages in flight in parallel for
improved performance. You can tune the max number of in flight messages with the
field `max_in_flight`.

## Fields

### `hosts`

A list of hosts to connect to.


Type: `string`  
Default: `["localhost:9000"]`  

```yaml
# Examples

hosts: localhost:9000
```

### `user`

A user identifier.


Type: `string`  
Default: `"benthos_hdfs"`  

### `directory`

A directory to store message files within. If the directory does not exist it will be created.


Type: `string`  
Default: `""`  

### `path`

The path to upload messages as, interpolation functions should be used in order to generate unique file paths.
This field supports [interpolation functions](/docs/configuration/interpolation#bloblang-queries).


Type: `string`  
Default: `"${!count(\"files\")}-${!timestamp_unix_nano()}.txt"`  

```yaml
# Examples

path: ${!count("files")}-${!timestamp_unix_nano()}.txt
```

### `max_in_flight`

The maximum number of messages to have in flight at a given time. Increase this to improve throughput.


Type: `number`  
Default: `1`  


