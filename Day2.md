# Day 2
Gives a basic introduction to data science and python nad a few popular libraries

Pandas is a Python library that allows us to manipulate, process, and structure data. Matplotlib allows us to quickly create a large variety of plots. For example, bar charts, histograms, pie charts, waterfalls, and all sorts.

Now onto the task,

1. Requires packet number, using given code and then the count function
   ```
   import pandas as pd
   import matplotlib.pyplot as plt
   df = pd.read_csv('network_traffic.csv')
   df.head(5)
   df.count()
   ```
gives result
```
PacketNumber    100
Timestamp       100
Source          100
Destination     100
Protocol        100
dtype: int64
```
So packet number : 100


2. The IP that sent the most amount of traffic, with given code we use df.groupby as follows

![Screenshot (101)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/32eb557b-2518-4bbd-ac8a-1dc063a6000e)

Most busy IP : 10.10.1.4


3. To find the most used protocol we used value_counts() function on the appropriate column as follows

![Screenshot (103)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/31bec3ee-3c7a-4403-9bb9-099d9898982f)

Most used protocol : ICMP


