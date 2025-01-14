---
title: Latency
---

# Latency and Throughput

Our approach to SQL performance benchmarking is to use `sysbench`, an
industry standard benchmarking tool.

## Performance Roadmap

Dolt is slower than MySQL. The goal is to get Dolt to match 
MySQL latency for common operations. Dolt is currently 2X slower 
than MySQL, approximately 1.5X on writes and 2.5X on reads. The 
`multiple` column represents this relationship with regard to a 
particular benchmark.

It's important recognize that these are industry standard tests, and
are OLTP oriented. Performance results may vary but Dolt is 
generally competitive on latency with MySQL and Postgres.

## Benchmark Data

### Current Default Format (`__DOLT__`)

Below are the results of running `sysbench` MySQL tests against Dolt
SQL Server for the most recent release of Dolt in the current default 
storage format. We will update this with every release. The tests 
attempt to run as many queries as possible in a fixed 2 minute time 
window. The `Dolt` and `MySQL` columns show the median latency in 
milliseconds (ms) of each query during that 2 minute time window.

The Dolt version is `1.13.5`.

<!-- START___DOLT___LATENCY_RESULTS_TABLE -->
|       Read Tests        | MySQL |  Dolt  | Multiple |
|-------------------------|-------|--------|----------|
| covering\_index\_scan   |  2.07 |   2.86 |      1.4 |
| groupby\_scan           | 12.98 |  17.95 |      1.4 |
| index\_join             |  1.27 |   4.74 |      3.7 |
| index\_join\_scan       |  1.21 |   2.26 |      1.9 |
| index\_scan             | 32.53 |  59.99 |      1.8 |
| oltp\_point\_select     |  0.14 |    0.4 |      2.9 |
| oltp\_read\_only        |  2.71 |    7.3 |      2.7 |
| select\_random\_points  |  0.31 |   0.72 |      2.3 |
| select\_random\_ranges  |  0.37 |   1.03 |      2.8 |
| table\_scan             | 33.12 |  59.99 |      1.8 |
| types\_table\_scan      | 74.46 | 173.58 |      2.3 |
| reads\_mean\_multiplier |       |        |      2.3 |

|       Write Tests        | MySQL | Dolt  | Multiple |
|--------------------------|-------|-------|----------|
| bulk\_insert             | 0.001 | 0.001 |      1.0 |
| oltp\_delete\_insert     |  4.65 |  5.57 |      1.2 |
| oltp\_insert             |  2.18 |  2.71 |      1.2 |
| oltp\_read\_write        |  6.09 | 14.21 |      2.3 |
| oltp\_update\_index      |   2.3 |  2.81 |      1.2 |
| oltp\_update\_non\_index |  2.35 |  2.81 |      1.2 |
| oltp\_write\_only        |  3.25 |  7.04 |      2.2 |
| types\_delete\_insert    |  4.65 |  5.88 |      1.3 |
| writes\_mean\_multiplier |       |       |      1.5 |

| Overall Mean Multiple | 1.9 |
|-----------------------|-----|
<!-- END___DOLT___LATENCY_RESULTS_TABLE -->
<br/>
