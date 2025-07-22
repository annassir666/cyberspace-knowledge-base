#networks

If you are wondering, a subnet mask of **`255.255.255.0`** can also be written as **`/24` (**192.168.66.89/24**)**. The **`/24`** means that the leftmost 24 bits within the IP address do not change across the network, i.e., the subnet. In other words, the leftmost three octets are the same across the whole subnet; therefore, we can expect to find addresses that range from **`192.168.66.1`** to **`192.168.66.254`**. Similar to what was mentioned earlier, **`192.168.66.0`** and **`192.168.66.255`** are the network and broadcast addresses, respectively.

RFC 1918 defines the following three ranges of private IP addresses:

- **`10.0.0.0`** - **`10.255.255.255`** (**`10/8`**)
- **`172.16.0.0`** - **`172.31.255.255`** (**`172.16/12`**)
- **`192.168.0.0`** - **`192.168.255.255`** (**`192.168/16`**)