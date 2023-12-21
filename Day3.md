# Day 3
*** Use of crunch and Hydra ***
**********
We will use Crunch, a tool that generates a list of all possible password combinations based on given criteria. We need to issue the following command:

`crunch 3 3 0123456789ABCDEF -o 3digits.txt`

The command above specifies the following:

1. 3 the first number is the minimum length of the generated password
2. 3 the second number is the maximum length of the generated password
3. 0123456789ABCDEF is the character set to use to generate the passwords
4. -o 3digits.txt saves the output to the 3digits.txt file

Hydra is an automated tool to try out generated passwords. 

Before we start, we need to view the page’s HTML code. We can do that by right-clicking on the page and selecting “View Page Source”. You will notice that:

1. The method is post
2. The URL is http://MACHINE_IP:8000/login.php
3. The PIN code value is sent with the name pin

syntax:

`hydra -l '' -P 3digits.txt -f -v MACHINE_IP http-post-form "/login.php:pin=^PASS^:Access denied" -s 8000`

The command above will try one password after another in the 3digits.txt file. It specifies the following:

1. -l '' indicates that the login name is blank as the security lock only requires a password
2. -P 3digits.txt specifies the password file to use
3. -f stops Hydra after finding a working password
4. -v provides verbose output and is helpful for catching errors
5. MACHINE_IP is the IP address of the target
6. http-post-form specifies the HTTP method to use
7. "/login.php:pin=^PASS^:Access denied" has three parts separated by :
   1. /login.php is the page where the PIN code is submitted
   2. pin=^PASS^ will replace ^PASS^ with values from the password list
   3. Access denied indicates that invalid passwords will lead to a page that contains the text “Access denied”
8. -s 8000 indicates the port number on the target

************

Now we move onto the challenge,

First we visit the machine IP, http://10.10.20.138:8000/ , it takes a 3 digit pin with a character set 0123456789ABCDEF, on inspecting the page we can fnd out the HTML method used, login page url, and the name assigned to the pin.

![VirtualBox_Ayan_21_12_2023_19_38_06](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/4938c5ea-40f4-4b90-bafd-459d389cd756)


Now we use to crunch to make the passwords dataset

![VirtualBox_Ayan_21_12_2023_19_39_49](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/a7767f11-56f6-4796-a17e-4958ea65dbfc)

Now we install and run hydra using given syntax, and we get the password : "6F5"

Log into the machine and unlock the door to get the flag : "THM{pin-code-brute-force}"

![VirtualBox_Ayan_21_12_2023_19_48_13](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/d642e571-48b4-4005-80eb-3067ce04689b)


