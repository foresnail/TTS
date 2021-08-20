# Telemetry-based Time-synchronization System
Nanosecond-level Time Synchronization based on Telemetry

"clone_test_zcf.p4" is the P4 data-plane program for the tofino programmable switch, which defines the data-plane forwarding logic of intermediate nodes in TTS: Each intermediate node records the receive and transmit timestamp of packets in the packet header. The last intermediate node sends the timestamp data recorded in the path to the upper Telemetry Controller for synchronization, and sends the original packet with timestamps removed to the end node for normal communication. (As shown in Fig.1.)

<img src="/images/figure5.png" height = "500" align=center>

"ctrl_clone_test_zcf.py" is the control-plane test program of the programmable switch. Through this program, the switch ports are started up and the flow table is configured. We have performed experiments with multiple hops apart and at different link rates, and results show that the nodes can achieve high-precision time synchronization at the nanosecond level.

A test result between multiple hops is shown in "clone_4hop.pcap" (time synchronization between nodes that are 4 hops apart). The pcap file has a total of 100,000 data packets, which are logical 50,000 pairs of data packets (the first 50,000 packets are logical request packets, and the last 50,000 are logical reply packets), the timestamps of entering and leaving each intermediate node have been recorded in the packet header. Based on the file, Telemetry Controller can calculate the offset according to 50,000 pairs of time data. After removing the outliers, the calculated value will be compared with the actual offset (i.e., 0), and the offset error is just 2.06 nanoseconds. (Corresponding to Fig.2., when the nodes are 4 hops apart and the offset is calculated with Eq.5 combined with LOF algorithm.)
![avatar](/images/figure9.png){:height="50%" width="50%"}
