# Day 4
*** Usage of CeWL ***

*************
CeWL is a custom wordlist generator that generates a list of potential passwords, by spidering. Spidering, in the context of web security and penetration testing, refers to the process of automatically navigating and cataloguing a website's content, often to retrieve the site structure, content, and other relevant details. It can also make a list of email addresses and usernames.

CeWL provides a lot of options that allow you to tailor the wordlist to your needs:

1. Specify spidering depth: The -d option allows you to set how deep CeWL should spider. For example, to spider two links deep: cewl http://MACHINE_IP -d 2 -w 
   output1.txt
2. Set minimum and maximum word length: Use the -m and -x options respectively. For instance, to get words between 5 and 10 characters: cewl http://MACHINE_IP -m 5 - 
   x 10 -w output2.txt
3. Handle authentication: If the target site is behind a login, you can use the -a flag for form-based authentication.
4. Custom extensions: The --with-numbers option will append numbers to words, and using --extension allows you to append custom extensions to each word, making it 
   useful for directory or file brute-forcing.
5. Follow external links: By default, CeWL doesn't spider external sites, but using the --offsite option allows you to do so.

************

Now onto the challenge,

