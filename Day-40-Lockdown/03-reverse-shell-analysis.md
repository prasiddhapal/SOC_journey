# Day 40 - Reverse Shell Analysis

## Objective

Identify the listening port used for the reverse shell and connect the network evidence to the compromised IIS process.

## Q5 - Reverse Shell Port

Initial destination-port frequency was noisy because normal TCP traffic was mixed with the reverse-shell connection.

The investigation was narrowed to initial SYN traffic from the IIS host to the attacker:

```bash
tshark -r capture.pcapng -Y "ip.src == 10.0.2.15 && ip.dst == 10.0.2.4 && tcp.flags.syn==1 && tcp.flags.ack==0" -T fields -e frame.time -e ip.src -e ip.dst -e tcp.dstport
```

The relevant connection showed:

```text
10.0.2.15 → 10.0.2.4 : 4443
```

### Q5 Answer

```text
4443
```

## Process Context

The memory investigation later identified the IIS worker process:

```text
w3wp.exe
```

with PID:

```text
4332
```

This provided endpoint context for the reverse-shell activity.

## Key Lesson

A high-frequency port is not automatically the reverse shell. Filter by direction, TCP state, timing, and the expected source/destination relationship.
