# Day 1 (Machine Learning)
Here we are taught about Natural Language processing in AI chatbots, prompt injection attacks and defense against them.

First we connect to the chatbot van chatty through given instructions start machine and connect to url after waiting 3min

1. For our first attack, we ask the chatbot outright for sensitive information, sometimes there's no security on this data and can we obtained easily, this happpens due to how chatbots are trained, learning from vast databases, so if we give an AI corporate info, it can leak it if prompted.

![AoC-d1](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/497582de-f5a5-4d9e-810e-8139f8069818)

2. Now here, the devs have indeed placed some security measures for the IT room door pass, which says that only authorized personnel can access it, but this can be bypassed. The chatbot can be tricked by asking it in a way that tells that we are a member of the IT team, or just ask the list of IT team members take on of the names and ask the password and the chatbot gives it to ya.

![AoC-d1,1](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/7fc1cf21-7a60-47ee-9d0c-4a0e9661069a)

3. Another protection measure is to use another AI called interceptor which scans prompts for malicious intent before letting the chatbot answer it, this a very good measure but it can be bypassed by attacks it has never seen before, the way we use here is to tell the chatbot that its in maintainence mode and then ask for the informations. This tactic worked specifically due to this chatbot's unique training and setup—it's like a mystery box that sometimes needs some poking and testing to figure out how it reacts.

![AoC-d1,2](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/12a5ea3a-76a3-4e49-b7df-5f3d00bcb990)

One shoild remember that problems in cyber are specific and what works at one place doesn't work on the other.

McGreedy's personal email : t.mcgreedy@antarcticrafts.thm

IT server room door pass : BtY2S02

McGreedy's secret project name : Purple Snow
