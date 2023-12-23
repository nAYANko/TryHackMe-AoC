# Day 6
In this challenge we learn to exploit a bug due to buffer overflow.

![Screenshot (115)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/0f723ddb-4f28-49bb-af20-9766941a4443)

******************
![Screenshot (116)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/e735c6fb-409a-407a-9598-d4bf940182c9)

The bug we have is after getting 13 coins and changing your name to "scroogerocks!" your suddenly get 33 coins

![Screenshot (118)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/0ddb9fcd-62fb-49ed-9167-da5ce1d1ab0d)

Using the debugger panel, we find out that the name variable can only store 12 bytes and when we store a name thats larger that that for example scroogerocks! which has 13 bytes it overflows to adjacent memory spaces, changing our names to aaaabbbbbccccx which leads to 120 coins as the memory space of coins variable now holds 78 and 0x78 is 120 in decimals. 

![Screenshot (120)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/fb0f1e91-e24e-429a-aca2-c9415f2f3e28)

![Screenshot (121)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/8e18bed3-9cbc-4a43-9269-e9a892b6c835)

The game doesn't check if the player_name variable has enough space to store the new name, it keeps on overwriting to adjacent memory space. This vulnerability is known as a buffer overflow and can be used to corrupt memory right next to the vulnerable variable.

Buffer overflows occur in some programming languages, mostly C and C++, where the variables' boundaries aren't strict. This games is made in C++.

Then restarting the game and naming yourself Elf, we can see the name is written byte by byte to the momory space followed by a red 0 which indicates a null value, the game ignores everything succeding the null value.

![Screenshot (122)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/fedd8fba-452b-42e1-be46-c8a4509e3acb)

Getting 16 coins and changing name to AAAABBBBCCCCDDDD leads to the null value to be places as the first byte in shopk_name variable and hence the game ignores everything after it and hence the shopkeeper name now appears to be blank.

![Screenshot (123)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/ac856422-6716-45de-8117-00bc4573eca6)

Changing name to AAAABBBBCCCCDEFG leads to 1195787588 coins. Now the value of bytes in coins variable is '44 45 46 47' which doesn't match the coins value when converted to decimal, we learn that integers in C++ are stored in a very particular way in memory. First, integers have a fixed memory space of 4 bytes, as seen in the debug panel. Secondly, an integer's bytes are stored in reverse order in most desktop machines. This is known as the little-endian byte order. Converting the current coin count to hex gives us 0x(47 46 45 44) corresponding to what's shown by the debug panel but backwards.

![Screenshot (129)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/0d9eadf7-1d87-4696-b651-e55905fcb4f1)
********************

Now we move to the challenge,

The number of coins when variable stores 4f 4f 50 53 is 0x(53 50 4f 4f) in decimal which is 1397772111.

If we try to buy the star from the shopkeeper, we are denied as follows which proves that the game is actually rigged.

![Screenshot (124)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/b01e6f59-58f6-41e6-92a6-e671bd6d3ed1)

![Screenshot (125)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/f941dd6f-8aed-43da-9ff7-5969c1c7889a)

![Screenshot (126)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/ae211a02-18c5-4bf0-91ac-592226fc794e)

![Screenshot (127)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/055fc87a-ef4e-445f-a409-a99241b17048)

The item he gives us is of no use.

To solve the challenge, we need to overflow the memory till it reaches the inv_items variable and then make that byte as " d " , which is the item id for the star.
The star automatically appears in the inventory. Give it the tree to get the flag : "THM{mchoneybell_is_the_real_star}"

![Screenshot (130)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/8ff72561-2148-44f6-8683-7e21dd72fb50)

![Screenshot (131)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/41736151-ec24-4ce2-9335-5214fed18016)

![Screenshot (132)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/99253ebc-7c38-49be-b28b-f6aa937a60e1)



