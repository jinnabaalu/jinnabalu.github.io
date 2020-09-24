---
layout: post
title:  "Tombstones in Cassandra - Clean"
description: "Cleaning the tomb_stones in cassandra with GC_GRACE_SECONDS for the table"
author: jinnabalu
categories: [ Cassandra, NoSQL, Storage ]
tags: [red, yellow]
image: assets/images/Cassandra_gc_grace_seconds.png
featured: true
hidden: true
---

Tombstones costs disk utilization and increased query time. Monitoring the amount of tombstoned data is an important part of monitoring the health of a Cassandra cluster. We can use the SSTablemetadata command to get information on a particular table’s tombstone ratio. We can simply clear the tombstoned data in cassandra by altering ths <code>GC_GRACE_SECONDS</code>

# Clean tombstones in cassandra

- Get the GC_GRACE_SECONDS value of the table, store it in some file.

- Alter to reduce the GC_GRACE_SECONDS to 30 

`alter table student with GC_GRACE_SECONDS = 30;`

Wait for 30-60 seconds to cleanup the tombstones and continue to alter to the last value.

- Replace it back with actual value

`alter table student with GC_GRACE_SECONDS = 86400;`
