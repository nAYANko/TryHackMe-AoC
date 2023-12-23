# Day 6
In this challenge we learn to exploit a bug due to buffer overflow.

******************

The bug we have is after getting 13 coins and changing your name to "scroogerocks!" your suddenly get 33 coins

Using the debugger panel, we find out that the name variable can only store 12 bytes and when we store a name thats larger that that for example scroogerocks! which has 13 bytes it overflows to adjacent memory spaces, changing our names to aaaabbbbbccccx which leads to 120 coins as the memory space of coins variable now holds 78 and 0x78 is 120 in decimals. 

The game doesn't check if the player_name variable has enough space to store the new name, it keeps on overwriting to adjacent memory space. This vulnerability is known as a buffer overflow and can be used to corrupt memory right next to the vulnerable variable.

Buffer overflows occur in some programming languages, mostly C and C++, where the variables' boundaries aren't strict. This games is made in C++.

Then restarting the game and naming yourself Elf, we can see the name is written byte by byte to the momory space followed by a red 0 which indicates a null value, the game ignores everything succeding the null value.

Getting 16 coins and changing name to AAAABBBBCCCCDDDD leads to the null value to be places as the first byte in shopk_name variable and hence the game ignores everything after it and hence the shopkeeper name now appears to be blank.

Changing name to AAAABBBBCCCCDEFG leads to 1195787588 coins. Now the value of bytes in coins variable is '44 45 46 47' which doesn't match the coins value when converted to decimal, we learn that integers in C++ are stored in a very particular way in memory. First, integers have a fixed memory space of 4 bytes, as seen in the debug panel. Secondly, an integer's bytes are stored in reverse order in most desktop machines. This is known as the little-endian byte order. Converting the current coin count to hex gives us 0x(47 46 45 44) corresponding to what's shown by the debug panel but backwards.

********************

The number of coins when variable stores 4f 4f 50 53 is 0x(53 50 4f 4f) in decimal which is 1397772111.

If we try to buy the star from the shopkeeper, we are denied as follows which proves that the game is actually rigged.

To solve the challenge, we need to overflow the memory till it reaches the inv_items variable and then make that byte as " d " , which is the item id for the star.
The star automatically appears in the inventory. Give it the tree to get the flag : "THM{mchoneybell_is_the_real_star}"

