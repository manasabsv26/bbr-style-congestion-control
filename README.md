## BBR (Bottleneck Bandwidth and Round-trip propagation time) Style Congestion Control Algorithm

Developed a BBR-style congestion control algorithm as part of the CSCI-551 Computer Networks course at the University of Southern California (USC); the source code cannot be publicly shared due to course academic policies. This implementation is based on the BBR congestion control algorithm described by Cardwell et al. in:
```
P9. [Cardwell17a] Neal Cardwell, Yuchung Cheng, C. Stephen Gunn, Soheil Hassas Yeganeh, and Van
Jacobson. BBR: Congestion-based congestion control. Communications of the ACM, 60(2):58–66, February
2017. (https://dl.acm.org/doi/10.1145/3009824)
```

## Why BBR?

Traditional congestion control algorithms like TCP Reno rely on packet loss as a signal for congestion, which often leads to buffer buildup, increased latency, and inefficient bandwidth utilization. BBR takes a different approach by modeling the network and estimating key network parameters instead of reacting after congestion occurs. This allows it to achieve higher throughput while maintaining lower latency.

## What does BBR do?

BBR models the network using two key parameters:

- **Bottleneck Bandwidth (BtlBw)** – the maximum delivery rate observed  
- **Round-trip propagation time (RTprop)** – the minimum observed RTT  

Using these, it estimates the **bandwidth-delay product (BDP)** and controls:

- **Pacing rate** → how fast packets are sent  
- **Congestion window** → how much data is in flight  

### BBR Phases

- **STARTUP**: rapidly probes for available bandwidth  
- **PROBE_BW**: maintains and probes around the estimated bandwidth  
- **PROBE_RTT**: periodically refreshes RTT estimates  

BBR keeps the network pipe full while avoiding large queue buildup.

This project implements a BBR-style congestion control algorithm; more details can be found in the report.

## Sample Execution Outputs

`Phase Logs` : Phase logs show how bandwidth and RTT estimates evolve over time, along with state transitions (e.g., STARTUP → PROBE_BW). These logs help verify that the algorithm correctly identifies the bottleneck bandwidth and stabilizes.

`Time-Sequence Diagrams`: Time-sequence plots visualize how packets are sent and acknowledged over time

1. BBR time-sequence plot showing STARTUP behaviour followed by transition to steady PROBE_BW
   

<img width="900" height="622" alt="bytes-zoomed-in" src="https://github.com/user-attachments/assets/0ce14af2-124b-448e-be11-6f610ebcbec3" />



2. Phase log showing the evolution of bandwidth and RTT estimates over time


<img width="830" height="215" alt="phase-log" src="https://github.com/user-attachments/assets/61de426c-24f2-404a-8caf-0613aeeccbf7" />



3. Baseline setup with a single BBBROC flow (one sender and one receiver), fully utilizing the bottleneck
bandwidth


<img width="922" height="495" alt="bbbroc-bw" src="https://github.com/user-attachments/assets/98baa7a6-608b-483e-a551-efab728f3619" />

### More Details

A detailed explanation of the implementation, experiments, and analysis is available in the full report.


