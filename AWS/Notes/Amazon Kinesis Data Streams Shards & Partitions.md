Amazon Kinesis Data Streams collect and process data in real time. A _Kinesis data stream_ is a set of [shards](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#shard). Each shard has a sequence of data records. Each data record has a [sequence number](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#sequence-number) that is assigned by Kinesis Data Streams. A _shard_ is a uniquely identified sequence of data records in a stream.

A _partition key_ is used to group data by shard within a stream. Kinesis Data Streams segregates the data records belonging to a stream into multiple shards. It uses the partition key that is associated with each data record to determine which shard a given data record belongs to.

![](https://digitalcloud.training/wp-content/uploads/2020/05/Picture-1-35.jpg)
