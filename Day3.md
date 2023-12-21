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





