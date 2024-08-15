# ⏱️ Latency Comparison (Approx. ~2012)

| Operation                                      | Latency          |
|------------------------------------------------|------------------|
| L1 Cache Reference                             | 0.5 ns           |
| Branch Mispredict                              | 5 ns             |
| L2 Cache Reference                             | 7 ns             |
| Mutex Lock/Unlock                              | 25 ns            |
| Main Memory Reference                          | 100 ns           |
| Compress 1K Bytes with Zippy                   | 3,000 ns         |
| Send 1K Bytes over 1 Gbps Network              | 10,000 ns        |
| Read 4K Randomly from SSD*                     | 150,000 ns       |
| Read 1 MB Sequentially from Memory             | 250,000 ns       |
| Round Trip within Same Datacenter              | 500,000 ns       |
| Read 1 MB Sequentially from SSD*               | 1,000,000 ns (1 ms) |
| Disk Seek                                      | 10,000,000 ns (10 ms) |
| Read 1 MB Sequentially from Disk               | 20,000,000 ns (20 ms) |
| Send Packet CA -> NH -> CA                     | 150,000,000 ns (150 ms) |

*Note: SSD refers to Solid State Drives.*
