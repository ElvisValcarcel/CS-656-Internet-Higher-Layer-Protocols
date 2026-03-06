# CS656 Midterm 1 Formulas March 6, 2026

## Ch 1: Delays & Throughput

| Metric | Formula | Variables |
|---|---|---|
| **Traffic intensity** | I = La / R | *L* = pkt size [bits/pkt], *a* = arrival rate [pkts/s], *R* = tx rate [bits/s]. As I → 1, queuing delay → ∞. |
| **Transmission delay** | Node: d_trans = L / R · End-to-end: d_trans = NL / R | *N* = number of nodes |
| **Propagation delay** | d_prop = d / s | *d* = distance [m], *s* = speed of light [m/s] |
| **Queuing delay** | d_queue = I·(L/R) / (1 − I) | *I* = traffic intensity |
| **Total nodal delay** | d_nodal = d_proc + d_queue + d_trans + d_prop | |
| **E2E throughput** | min{R₁, R₂, …, Rₙ} | Bottleneck link determines throughput (single src/dst). |

## Ch 2: File Distribution

| Model | Formula | Notes |
|---|---|---|
| **Client-server** | D_cs ≥ max{ NF/u_s , F/d_min } | *N* = peers, *F* = file size [bits], *u_s* = server upload [bits/s], *d_min* = min peer download. Scales **linearly** with N. (≥ often =) |
| **Peer-to-peer** | D_P2P ≥ max{ F/u_s , F/d_min , NF/(u_s + Σuᵢ) } | *uᵢ* = upload rate of peer *i*. Server sends one copy; peers redistribute. Scales **much slower** than C/S. (≥ often =) |

## Ch 3: TCP & Reliability

| Metric | Formula | Variables / Notes |
|---|---|---|
| **Utilization (stop-wait)** | U_sender = (L/R) / (RTT + L/R) | *L* = pkt size, *R* = tx rate, *RTT* = round-trip time |
| **Utilization (pipelined)** | U_sender = N·(L/R) / (RTT + L/R) | *N* = pkts sent before ACK |
| **EstimatedRTT** | (1−α)·EstRTT + α·SampleRTT | EWMA; recommended α = 0.125 |
| **DevRTT** | (1−β)·DevRTT + β·\|SampleRTT − EstRTT\| | EWMA; recommended β = 0.25 |
| **Timeout interval** | EstRTT + 4·DevRTT | Init = 1s. Doubled after timeout; recalculated after ACK. |
| **TCP send rate** | cwnd / RTT | *cwnd* = congestion window [bytes] |
| **Receive window** | rwnd = RcvBuffer − (LastByteRcvd − LastByteRead) | Spare room in receive buffer. RcvBuffer ≥ LastByteRcvd − LastByteRead |
| **Unacked data limit** | LastByteSent − LastByteAcked ≤ min{cwnd, rwnd} | |
| **Reno avg throughput** | 0.75·W / RTT | *W* = max cwnd at loss event [bytes] |
| **Avg rate w/ loss** | ≈ 1.22·MSS / (RTT·√L) | *MSS* = max segment size, *L* = loss rate |
