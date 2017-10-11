# gossipdb
Distributed Embedded Key-Value store

## What it does?
An in memory cache which listens to neighbouring nodes and replicates
messages using gossip protocol.

gossipdb provides the replication and in-memory persistance layer for
the nodes of the cluster. It provides APIs to put and fetch data in
a key value pair. It also provides an API to fetch the active members of the cluster.

## Example

The 'example' directory contains an example application which has can be
used to add keys using an API call and fetching it from any of the
nodes.

You can build the example using the following steps:
```
cd example
glide install
go build
```

You then need to run two instances of the app on different tabs of your
terminal:
```
./example -http_port 8000 -rpc_port 9000 -members
'0.0.0.0:9000,0.0.0.0:9001'

./example -http_port 8001 -rpc_port 9001 -members
'0.0.0.0:9000,0.0.0.0:9001'
```

Sample payload for the '/add_key' API is shown below:
```
{
"key": "ping",
"value": "pong"
}
```

The key can then be fetched by using the query '/value?key=ping' 

## Roadmap

GossipDb is currently an early alpha project. Api interface is likely to
change, and is not recommended for production usages.

Todos
1. Improve test coverage
2. CI pipeline and code linting tools
3. Config Objects for DB
4. Better capability from Key-Value store, like ttl, and deletes
5. Improved Object parser
6. Cluster health and Status
7. Instrumentation on replication
8. Benchmarking
9. Example usage

## Building

CI Status: ![Travis CI](https://travis-ci.org/SinisterLight/gossipdb.svg?branch=master)

```
try,
  make init
  make deps
  make test (or clean)
or,
  make
```

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
