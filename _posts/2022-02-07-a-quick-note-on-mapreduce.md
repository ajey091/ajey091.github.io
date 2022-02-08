---
layout: post
image: /assets/images/Test_image.jpeg
---
MapReduce is a programming model and an associated implementation for processing and generating big data sets with a parallel, distributed algorithm on a cluster. Alternatively, MapReduce is a framework for processing parallelizable problems across large datasets using nodes. Processing can occur on data stored either in a filesystem (unstructured) or in a database (structured). MapReduce can take advantage of the locality of data, processing it near the place it is stored in order to minimize communication overhead.

A MapReduce program is composed of a map procedure, which performs filtering and sorting (such as sorting students by first name into queues, one queue for each name), and a reduce method, which performs a summary operation (such as counting the number of students in each queue, yielding name frequencies).

The model is a specialization of the split-apply-combine strategy for data analysis. It is inspired by the map and reduce functions commonly used in functional programming, although their purpose in the MapReduce framework is not the same as in their original forms. As such, a single-threaded implementation of MapReduce is usually not faster than a traditional (non-MapReduce) implementation; any gains are usually only seen with multi-threaded implementations on multi-processor hardware. The use of this model is beneficial only when the optimized distributed shuffle operation (which reduces network communication cost) and fault tolerance features of the MapReduce framework come into play. Optimizing the communication cost is essential to a good MapReduce algorithm.

A popular open-source implementation that has support for distributed shuffles is part of Apache Hadoop.

### Apache Hadoop vs Apache Spark

Apache Hadoop is an open-source software utility that allows users to manage big data sets using nodes to solve data problems. It is a highly scalable, cost-effective solution that stores and processes structured, semi-structured and unstructured data (e.g., Internet clickstream records, web server logs, IoT sensor data, etc.).

Like Hadoop, Apache Spark splits up large tasks across different nodes. However, it tends to perform faster than Hadoop and it uses RAM to cache and process data instead of a file system. This enables Spark to handle use cases that Hadoop cannot.
