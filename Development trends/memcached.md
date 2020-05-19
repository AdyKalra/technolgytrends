### Memcached
* Memcached is a **general-purpose distributed memory-caching system.** It is often used to **speed up dynamic database-driven websites by caching data and objects in RAM to reduce the number of times an external data source must be read**. Memcached is free and **open-source** software
* Memcached stores data based on key-values for small arbitrary strings or objects including: Results of database calls.
* On a fast machine with very high speed networking, memcached can easily handle 200,000+ requests per second. With heavy tuning or even faster hardware it can go many times that. Hitting it a few hundred times per second, even on a slow machine, usually isn't cause for concern
* memcached is multi-threaded by default and has no problem saturating many cores. ... This option is only meaningful if memcached was compiled with thread support enabled. It is typically not useful to set this higher than the number of CPU cores on the memcached server.

### WHAT ARE SOME ALTERNATIVES TO MEMCACHED?
* Redis
Redis is an open source, BSD licensed, advanced key-value store. It is often referred to as a data structure server since keys can contain strings, hashes, lists, sets and sorted sets.
* Ehcache
Ehcache is an open source, standards-based cache for boosting performance, offloading your database, and simplifying scalability. It's the most widely-used Java-based cache because it's robust, proven, and full-featured. Ehcache scales from in-process, with one or more nodes, all the way to mixed in-process/out-of-process configurations with terabyte-sized caches.
* Varnish
Varnish Cache is a web application accelerator also known as a caching HTTP reverse proxy. You install it in front of any server that speaks HTTP and configure it to cache the contents. Varnish Cache is really, really fast. It typically speeds up delivery with a factor of 300 - 1000x, depending on your architecture.
* Hazelcast
With its various distributed data structures, distributed caching capabilities, elastic nature, memcache support, integration with Spring and Hibernate and more importantly with so many happy users, Hazelcast is feature-rich, enterprise-ready and developer-friendly in-memory data grid solution.
* MongoDB
MongoDB stores data in JSON-like documents that can vary in structure, offering a dynamic, flexible schema. MongoDB was also designed for high availability and scalability, with built-in replication and auto-sharding.
