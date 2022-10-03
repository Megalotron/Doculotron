---
sidebar_position: 2
---

# PCAP streaming

The PCAP format is a file format used to store network traffic, it is used by many tools to store network traffic and to replay it.

It is a binary file format, it is composed of a header and a list of packets.

## Packet record

A Packet Record is the standard container for storing the packets coming from the network.

```
   0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
 0 |                      Timestamp (Seconds)                      |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
 4 |            Timestamp (Microseconds or nanoseconds)            |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
 8 |                    Captured Packet Length                     |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
12 |                    Original Packet Length                     |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
16 /                                                               /
   /                          Packet Data                          /
   /                        variable length                        /
   /                                                               /
   +---------------------------------------------------------------+
```
**The meaning of the fields in the Packet Record is:**

`Timestamp (Seconds)` and `Timestamp (Microseconds or nanoseconds)`:
seconds and fraction of a seconds values of a timestamp.

The seconds value is a 32-bit unsigned integer that represents the number of seconds that have elapsed since 1970-01-01 00:00:00 UTC, and the microseconds or nanoseconds value represents the number of microseconds or nanoseconds that have elapsed since that seconds.

Whether the value represents microseconds or nanoseconds is specified by the magic number in the File Header.

`Captured Packet Length` (32 bits):
an unsigned value that indicates the number of octets captured from the packet (i.e. the length of the Packet Data field). It will be the minimum value among the Original Packet Length and the snapshot length for the interface.

`Original Packet Length` (32 bits):
an unsigned value that indicates the actual length of the packet when it was transmitted on the network. It can be different from the Captured Packet Length if the packet has been truncated by the capture process.

`Packet Data`:
the data coming from the network, including link-layer headers. The actual length of this field is Captured Packet Length. The format of the link-layer headers depends on the LinkType field specified in the file header.

## The GRPC protocol

The sniffer uses the gRPC protocol to send the packets to go-flowmeter.
The following protobuf definition is used to send the packets:

```proto
message PacketHeader {
    uint32 ts_sec = 1;
    uint32 ts_usec = 2;
    uint32 caplen = 3;
    uint32 len = 4;
}

message PacketData {
    bytes data = 1;
}

message Packet {
    PacketHeader header = 1;
    PacketData data = 2;
}
```

The following method is used to start the stream:

```proto
service PacketStreaming {
    rpc Run(stream Packet) returns (google.protobuf.Empty);
}
```