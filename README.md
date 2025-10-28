
***

# Computer Networks Assignment 2

***

## Table of Contents

- [Part Breakdown](#part-breakdown)
  - [PART_A: Network Topology Setup](#part_a-network-topology-setup)
  - [PART_B: Default Resolver Experiments](#part_b-default-resolver-experiments)
  - [PART_C: Custom DNS Resolver](#part_c-custom-dns-resolver)
  - [PART_D: Custom DNS Server + Host Interface](#part_d-custom-dns-server-host-interface)
- [textfiles: Input Domain Lists](#textfiles-input-domain-lists)
- [Notes on JSON Files](#notes-on-json-files)
- [Analysis and Results](#analysis-and-results)
***

## Part Breakdown

### PART_A: Network Topology Setup

- **codewithnat.py** / **codewithoutnat.py**  
  - Scripts for setting up the Mininet emulated network, with/without NAT if outside network connectivity is desired.
- **README.md, commands.txt**  
  - Additional setup and usage information.

***

### PART_B: Default Resolver Experiments

For this part we need to change the /etc/resolv.conf file in your system to "nameserver 10.0.0.6'

- **host.py**  
  - Run on each Mininet host. Reads domain names from corresponding text files (see `textfiles/`). Resolves domains using the host's default system resolver (`getaddrinfo`) which directs to 10.0.0.6.
- **1PCAP.json, 2PCAP.json, ...**  
  - *Output statistics and resolved names and status for each host’s PCAP-derived domain list, using the default resolver.*
  - Contains statistics: latency, throughput, resolution status.
  - Contains resolved names

***

### PART_C: Custom DNS Resolver

Run this code on DNS server which will listen to any name resolution request from Hosts.

- **DNS_custom.py**  
  - Python implementation of a custom iterative DNS resolver (does the DNS walk itself).
  - Used to compare with the default resolver in PART_B.

***

### PART_D: Custom DNS Server + Host Interface

- **customresolver.py**  
  - Runs on the DNS node. Listens for DNS queries from hosts, performs iterative DNS resolution.
  - Stores per-query resolution paths, timings, etc.
- **host.py**  
  - Client code for host nodes—sends queries over UDP to the DNS server. Same as Part B
- **Resolver_no_cache_singleserver/**  
  - `PCAPX.json` files: JSON logs when only a single server is used, and no caching is present.
  - Marks all the information required by Part D of the question in json format

***

## textfiles: Input Domain Lists

- **temp_h1.txt ... temp_h4.txt**  
  - Clean lists of domains parsed from PCAP files via tshark, one for each host node.
  - Used as input for both default and custom resolver runs.

***

## Analysis and Results

- **Latencies, throughput, and cache hits** are logged and compared between default resolver runs (systemd, getaddrinfo) and custom iterative/server implementations.
- **Graphs and tables** are generated (see report PDF or notebook) using the output JSON logs.
- **Observations:**  
  - Default resolver is often faster due to direct recursive querying or system cache.
  - Custom resolver performance improves with cache and multi-server querying enabled.

***


