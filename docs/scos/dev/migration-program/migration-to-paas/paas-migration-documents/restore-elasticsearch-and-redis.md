---
title: Restore Elasticsearch and Redis
description: This document describes how to restore Elasticsearch and Redis data.
template: howto-guide-template
---

# Restore Elasticsearch and Redis

{% info_block infoBox %}

Resources: Backend

{% endinfo_block %}

As a platform for running restorable commands, we can use Jenkins. Just create a new Jenkins task with the commands
you want to execute, ensure it’s not scheduled to be executed frequently, and run them manually.

In case ElasticSearch and Redis are restorable via default Spryker tooling (this info is coming from prerequisites),
then the following command has to be executed:
```bash
console sync:data
```
Due to the big size of the data sometimes the command can not process all the records and fails. In this case,
it can be executed per resource:
```bash
console sync:data url
console sync:data product_concrete  
...
```
To see the list of available resources, run the command with `-h` flag:
```bash
console sync:data -h
```
Even running `sync:data` per resource sometimes is not efficient enough when the data size is really huge and the command
can not fit in dedicated resources/execution time limit. In this edge-case situation we can do a workaround by running
a trigger event command per heavy resource:
```bash
console publish:trigger-events -r product_abstract
```
To see the list of available resources, run the command with `-h` flag:
```bash
console publish:trigger-events -h
```
Usually triggering events is less resource intensive because it has to only push some ids into the queue, but the cons of
this synchronization approach are that it has to republish the data in `_storage` and `_search` tables of the resources
before it will be synchronized to Redis and ElasticSearch.

Ensure all messages are successfully consumed and RabbitMQ is empty.


