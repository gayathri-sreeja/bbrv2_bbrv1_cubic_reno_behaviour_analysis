#  BBRv2 vs BBRv1 vs CUBIC & Reno — TCP Congestion Control Behaviour Analysis

A detailed performance comparison of modern bandwidth-model-based TCP congestion control algorithms (BBRv1 & BBRv2) against loss-based algorithms (CUBIC and Reno) under multiple real-world network conditions.

---

##  Objective

The goal of this project is to analyse:

✔ Throughput & stability
✔ Latency / RTT behaviour
✔ Queueing performance under shallow & deep buffers
✔ Coexistence & fairness in mixed-flow environments
✔ Adaptiveness to bandwidth change
✔ Short vs long flow behaviour

BBRv2 promises fairness improvements over BBRv1 and reduced queue buildup.
This project experimentally evaluates how true that is.

---

##  Repository Structure

```
bbrv2_bbrv1_cubic_reno_behaviour_analysis/
│
├── run_mininet.py               # Main script to run experiments on Mininet
├── run_mininet_c_2.py           # Alternate experiment runner
├── Analyse.py                   # Data parsing & graph plotting
│
├── helper/                      # Utility scripts (log parsing, cleanup etc.)
│
├── install.sh                   # Setup script for environment
├── requirements.txt             # Python dependencies for analysis
│
├── buffer_script.sh             # Automates buffer behaviour experiments
├── ss_script.sh                 # Automates steady-state short-flow tests
│
├── *.conf                       # Configuration files for scenarios
│   ├── bbr_only.conf
│   ├── buffer_tests.conf
│   ├── bw_change.conf
│   ├── long_flows.conf
│   ├── mixed_flows.conf
│   ├── short_flows.conf
│   ├── short_long_rtt.conf
│
└── results/                     # Output graphs & stats (after execution)
```

---

##  Experimental Scenarios

| Scenario                  | Focus                                           |
| ------------------------- | ----------------------------------------------- |
|   BBR-only tests          | Stability & latency performance of BBR variants |
|   Mixed flows             | Fairness vs CUBIC/Reno at bottleneck            |
|   Buffer size variation   | Queue growth & packet loss pattern              |
|   Bandwidth change        | Responsiveness to dynamic networks              |
|   Short vs long flows     | Startup phase performance                       |
|   Different RTTs          | RTT-bias & flow dominance                       |

Metrics collected: throughput, queue occupancy, RTT, flow completion time, fairness index, etc.

---

## Setup & Installation

Requires:

* Linux (Kernel supporting BBRv1/v2, CUBIC, Reno)
* Mininet installed
* Root privileges

```bash
git clone https://github.com/gayathri-sreeja/bbrv2_bbrv1_cubic_reno_behaviour_analysis.git
cd bbrv2_bbrv1_cubic_reno_behaviour_analysis

sudo ./install.sh
pip install -r requirements.txt
```

---

##  Running Experiments

Example: Mixed congestion-control flow test

```bash
sudo python3 run_mininet.py --config mixed_flows.conf
```

###  Analyse Results

```bash
python3 Analyse.py --input logs/mixed_flows --output results/mixed_flows/
```

The script generates:

 Throughput graphs
 Latency & queue graphs
 Fairness comparisons

---

##  Key Questions This Study Answers

* Does BBRv2 handle fairness better than BBRv1?
* Does BBR starve loss-based flows in mixed environments?
* How much latency does each algorithm induce under shallow buffers?
* Which algorithm adapts faster to bandwidth shifts?
* What happens when short flows compete with long BBR streams?

---

##  Future Enhancements

* Support for new CCAs (e.g., BBRv3, PCC)
* Automated report generation for all experiments
* Real-hardware validation (testbed deployment)
* Jitter/loss injection for realistic networks
* Integration with ns-3 for simulation-grade results


