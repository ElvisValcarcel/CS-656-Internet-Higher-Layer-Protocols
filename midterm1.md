# CS656 Midterm 1 Formulas March 6, 2026

## Ch 1: Delays & Throughput

| Metric | Formula | Variables |
|---|---|---|
| **Traffic intensity** | $I = \frac{La}{R}$ | $L$ = pkt size [bits/pkt], $a$ = arrival rate [pkts/s], $R$ = tx rate [bits/s]. As $I \to 1$, queuing delay $\to \infty$. |
| **Transmission delay** | Node: $d_{trans} = \frac{L}{R}$ · E2E: $d_{trans} = \frac{NL}{R}$ | $N$ = number of nodes |
| **Propagation delay** | $d_{prop} = \frac{d}{s}$ | $d$ = distance [m], $s$ = speed of light [m/s] |
| **Queuing delay** | $d_{queue} = \frac{I \cdot (L/R)}{1 - I}$ | $I$ = traffic intensity |
| **Total nodal delay** | $d_{nodal} = d_{proc} + d_{queue} + d_{trans} + d_{prop}$ | |
| **E2E throughput** | $\min\{R_1, R_2, \ldots, R_N\}$ | Bottleneck link determines throughput (single src/dst). |

## Ch 2: File Distribution

| Model | Formula | Notes |
|---|---|---|
| **Client-server** | $D_{cs} \geq \max\lbrace\frac{NF}{u_s},\; \frac{F}{d_{min}}\rbrace$ | $N$ = peers, $F$ = file size [bits], $u_s$ = server upload [bits/s], $d_{min}$ = min peer download. Scales **linearly** with $N$. ($\geq$ often $=$) |
| **Peer-to-peer** | $D_{P2P} \geq \max\lbrace\frac{F}{u_s},\; \frac{F}{d_{min}},\; \frac{NF}{u_s + \sum_{i=1}^{N} u_i}\rbrace$ | $u_i$ = upload rate of peer $i$. Server sends one copy; peers redistribute. Scales **much slower** than C/S. ($\geq$ often $=$) |

## Ch 3: TCP & Reliability

| Metric | Formula | Variables / Notes |
|---|---|---|
| **Utilization (stop-wait)** | $U_{sender} = \frac{L/R}{RTT + L/R}$ | $L$ = pkt size, $R$ = tx rate, $RTT$ = round-trip time |
| **Utilization (pipelined)** | $U_{sender} = \frac{N \cdot L/R}{RTT + L/R}$ | $N$ = pkts sent before ACK |
| **EstimatedRTT** | $(1-\alpha)\cdot EstRTT + \alpha \cdot SampleRTT$ | EWMA; recommended $\alpha = 0.125$ |
| **DevRTT** | $(1-\beta)\cdot DevRTT + \beta \cdot \|SampleRTT - EstRTT\|$ | EWMA; recommended $\beta = 0.25$ |
| **Timeout interval** | $EstRTT + 4 \cdot DevRTT$ | Init = 1s. Doubled after timeout; recalculated after ACK. |
| **TCP send rate** | $\frac{cwnd}{RTT}$ | $cwnd$ = congestion window [bytes] |
| **Receive window** | $rwnd = RcvBuffer - (LastByteRcvd - LastByteRead)$ | Spare room in receive buffer. $RcvBuffer \geq LastByteRcvd - LastByteRead$ |
| **Unacked data limit** | $LastByteSent - LastByteAcked \leq \min\{cwnd,\; rwnd\}$ | |
| **Reno avg throughput** | $\frac{0.75 \cdot W}{RTT}$ | $W$ = max cwnd at loss event [bytes] |
| **Avg rate w/ loss** | $\approx \frac{1.22 \cdot MSS}{RTT\sqrt{L}}$ | $MSS$ = max segment size, $L$ = loss rate |

