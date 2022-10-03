---
sidebar_position: 1
---

# CLI

The sniffer can be used with CLI arguments, you can display the help menu with `--help` or `-h` arguments

```
sniffer 0.1.0
The sniffer of Megalotron

USAGE:
    sniffer [OPTIONS]

OPTIONS:
    -h, --help                     Print help information
    -i, --interface <INTERFACE>    Use a specific network interface instead of the default one
    -l, --logfile <LOGFILE>        If set, the logs will be save on the provided file
    -r, --read <READ>              Read packets from a pcap file instead of a network interface
    -u, --url <URL>                URL of the grpc server to send the pcap data stream
    -v, --verbosity <VERBOSITY>    Set the verbosity level [default: info]
    -V, --version                  Print version information
    -w, --write <WRITE>            Write captured packets on a pcap file
```

### Sniffing from a Network device

To collect network traffic from a specific network interface, use the `-i` or `--interface` argument:
```sh
sniffer -d eth0
```

### Sniffing from a Pcap file

To collect network traffic from a pcap file, use the `-r` or `--read` argument:

```sh
sniffer -r dataset.pcap
```

> :warning: Only one of the previous arguments can be used at the same time

### Write captured packets to a Pcap file

The sniffer can write the captured packets to a pcap file, to do so, use the `-w` or `--write` argument:

```sh
sniffer -w output.pcap
```

### Send data on a gRPC server

The sniffer sends the packets to a gRPC server, you can use the `-u` or `--url` arguments to specify the address of the server.

```sh
sniffer -u http://0.0.0.0:50051
```

### Set the verbosity level

The sniffer can set the verbosity level with the `-v` or `--verbosity` arguments, the possible values are: [debug, info, warn, error]

```sh
sniffer -v debug
```

### Save logs to a file

The sniffer can save the logs in a file, you can use the `-l` or `--logfile` arguments to specify the path of the file.

```sh
sniffer -l sniffer.log
```