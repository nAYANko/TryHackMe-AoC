# Day 7
We have to do a Log Analysis on a proxy server

****************

In a Log file entry like this one the terms are defined as

`158.32.51.188 - - [25/Oct/2023:09:11:14 +0000] "GET /robots.txt HTTP/1.1" 200 11173 "-" "curl/7.68.0"`

Source IP Address	- 158.32.51.188 - The source (computer) that initiated the HTTP request.

Timestamp	- [25/Oct/2023:09:11:14 +0000] - The date and time when the event occurred. 

HTTP Request - GET /robots.txt HTTP/1.1 - The actual HTTP request made, including the request method, URI path, and HTTP version.

Status Code	- 200	- The response of the web application.

User Agent - curl/7.68.0 - The user agent used by the source of the request. It is typically tied up to the application used to invoke the HTTP request.

PROXY SERVER

A proxy server is an intermediary between your computer or device and the internet. When you request information or access a web page, your device connects to the proxy server instead of connecting directly to the target server. The proxy server then forwards your request to the internet, receives the response, and sends it back to your device. It offers enhanced visibility into network traffic and user activities, since it logs all web requests and responses. This enables system administrators and security analysts to monitor which websites users access, when, and how much bandwidth is used. It also allows administrators to enforce policies and block specific websites or content categories.

LINUX COMMANDS DISCUSSION

CAT: Display the contents of single or multiple files, it shows all content till the end of file so it can become quite overwhelming for very large files.

![Screenshot (146)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/0081e418-43dd-4aa8-a2ae-2fea5107dbc3)

LESS: This command lets you view the contents of a file one at a time, either line by line or page by page, it makes the reviewing of logs less overwhelming, to navigate use up/down keys to move line by line and pageUp(b)/pageDown(space) to move page by page. Exit by pressing q.

HEAD: Lets you view contents on top of a file. Executing `head access.log` lets you view the first 10 entries of the log. To specify the number of lines typr -n followed by number of lines.

![Screenshot (147)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/342fa49e-3f83-459a-8bd4-524dcd735f09)

TAIL: This command allows you to view the end of the file. To display the last 10 entries of the log, execute `tail access.log` on the terminal. To specify the number of lines typr -n followed by number of lines. 

![Screenshot (148)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/18ab5150-1227-448b-8f0e-a92e1be5c3cc)

WC: The wc command stands for word count. It's a command-line tool that counts the number of lines, words, and characters in a text file. Try executing wc access.log. By default, it prints the count of lines, words, and characters as shown in your terminal. Use -l to display line count.

![Screenshot (149)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/615fdadc-7e8f-4069-9877-b470791ca57f)

NL: The nl command stands for number lines. It renders the contents of the file in a numbered line format.

![Screenshot (150)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/132d490e-f4dd-46ac-a06c-55b917e5bc68)

CONTENTS OF PROXY LOG

The proxy log in this server is configured as 

`` timestamp - source_ip - domain:port - http_method - http_uri - status_code - response_size - user_agent ``

For eg, taking the following entry: 

```
[2023/10/25:16:17:14] 10.10.140.96 storage.live.com:443 GET / 400 630 "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36"
```

Here,

Timestamp	- [2023/10/25:16:17:14]

Source IP	- 10.10.140.96

Domain and Port	- storage.live.com:443

HTTP Method	- GET

HTTP URI	- /

Status Code	- 400

Response Size	- 630

User Agent - "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36"

As you can see in the table above, we can break the log entry down and assign a position to each value so that it can be easily interpreted. The cut command allows you to extract specific sections (columns) of lines from a file or input stream by "cutting" the line into columns based on a delimiter and selecting which columns to display. This can be done using the -d option (for delimiter) and the -f for position. The example below uses space (' ') as its delimiter and only displays the timestamp (column #1 after cutting the log with space). 

```cut -d ' ' -f1 access.log```

![Screenshot (151)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/210a0308-6f64-4af0-9cf9-31203a157964)

We can select multiple coloums by seperating them by commas(,) in -f.

```cut -d ' ' -f1,3,6 access.log```

![Screenshot (152)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/0977029b-4b51-438a-8f13-7a14cafdd7f0)

The space delimiter won't work if you plan to get the User-Agent column since its value may contain a space, just like in the example log:

"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36"

Given this, you must change the delimiter and select column #2 because the User-Agent is enclosed with double quotes.

```cut -d '"' -f2 access.log```

![Screenshot (153)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/999f637b-c400-4045-9cd8-163200d430a9)

In the example above, we used column #2 since column #1 will provide the contents before the first use of double quotes ("). Try executing cut -d '"' -f1 access.log and see how the output differs from the space delimiter.

LINUX PIPES:

In Linux or Unix-like operating systems, a pipe (or the "|" character) is a way to connect two or more commands to make them work together seamlessly. It allows you to take the output of one command and use it as the input for another command. We'll introduce more commands by going through some use cases.

1. Get the first five connections made by 10.10.140.96.

To do this, we'll combine the grep command with the head command.

Grep is a command in Linux that is used for searching text within files or input streams. It typically follows the syntax: `grep OPTIONS STRING_TO_SEARCH FILE_NAME`.

Let's use the command to focus on the connections made by the specific IP by executing `grep 10.10.140.96 access.log`. To limit the display to the first five entries, we can append `| head -n 5` to that command to achieve our goal.

![Screenshot (154)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/06fbe2ea-1e63-44eb-b6a9-e8b595cd56c5)

The first command's output may have been a little too overwhelming since it provides every connection made by the specific IP. Meanwhile, appending a pipe with a head command limited the results to five.

2. Get the list of unique domains accessed by all workstations.

To do this, we'll combine the sort and uniq commands with the cut command.

Sort is a Linux command used to sort the lines of text files or input streams in ascending or descending order, while the uniq command allows you to filter out and display unique lines from a sorted file or input stream. 

Note: The uniq command requires a sorted list to be effective because it only compares the adjacent lines.

To achieve our goal, we will start by getting the domain column and removing the port. When we have the list of domains, we'll sort it and get the unique list using the sort and uniq commands.

3. Display the connection count made on each domain.

We already have the list of unique domains based on our previous use case. Now, we only need to add some parameters to our commands to get the count of each domain accessed. This can be done by adding the -c option to the uniq command.

```cut -d ' ' -f3 access.log | cut -d ':' -f1 | sort | uniq -c```

![Screenshot (155)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/6402efd1-77f1-4e57-8d9f-a1ffab925feb)

Moreover, the result can be sorted again based on the count of each domain by using the -n option for ascending and -r or -nr for descending of the sort command.

***************

Now moving onto the challenge,

We find the top 10 most visited domains by the user, You can do this by reusing the previous command to retrieve the connection count for each domain and 
`| tail -n 10` to get the last 10 items.

![Screenshot (156)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/eca2cf84-35ca-46c9-8b5d-3f6ea091e02a)

We see one suspicious domain i.e. frostlings.bigbadstash.thm, Upon checking the list of requests made to this domain, we see something unusual with the string passed to the `goodies` parameter. Let's try to retrieve the data by cutting the request URI with equals (=) as its delimiter.

![Screenshot (158)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/7abf3d63-3ba9-4acc-8164-d7b3888b85a3)

We pull the text using grep and the text is base64 encoded so we use `base64 -d` to get the decoded data which seems to be important.

![Screenshot (159)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/e4c02089-1e5f-4956-bf76-932436c057f7)

ANSWERS TO QUESTIONS::

1. No. of Unique IPs connected to the server - 9

    ```
    cut -d ' ' -f2 access.log | sort | uniq | nl
    ```

![Screenshot (160)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/b128c5a5-e18f-43c5-8941-a723ab86241d)

We use 2 in -f to get the IP column, piped with sort to sort all similar stuff together alphabetically, piped with uniq to remove all similar terms, piped with nl to number the lines. We see 9 different IPs.

2. No. of unique domains accessed by all work stations - 111

    ```
    cut -d ' ' -f3 access.log | cut -d ':' -f1 | sort | uniq | nl
    ```

![Screenshot (161)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/fce9cf0e-54a6-475b-be59-3547291a4a03)

The 3 in -f to get the Domain:port column, piped with another cut command with : delimiter and -f1 to get the Domain part ignoring the port, sort and uniq for their respective purpose and nl to number the lines. 111 unique domains.

3. Status code of the least accessed domain - 503

   First we find the least accessed domain which is partnerservices.getmicrosoftkey.com
   ```
    cut -d ' ' -f3 access.log | cut -d ':' -f1 | sort | uniq -c | sort -n
   ```

![Screenshot (162)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/2a745fff-8d36-4f49-881b-779742774e70)

   Then we grep that doamin, cut the status code column and then use uniq.
   ```
   grep partnerservices.getmicrosoftkey.com access.log | cut -d ' ' -f6 | uniq
   ```

![Screenshot (163)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/e4c9cfc3-e197-4657-ad8a-26b57e21f4c5)

4. Name of suspicious domain and IP of the workstation that accessed it - frostlings.bigbadstash.thm   10.10.185.225

![Screenshot (157)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/9b147ba9-9e6f-43b9-a6e6-ffe7d6796fb3)

5. Requests made to suspicious domain - 1581

![Screenshot (164)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/09ff9a4c-5650-4c21-92cf-e0ab90fe062e)

6. Getting the flag -  THM{a_gift_for_you_awesome_analyst!}
   
![Screenshot (165)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/922c127a-d8db-4a35-b600-c9ddc98f40ea)

Other way is to,
```
grep frostlings.bigbadstash.thm access.log | cut -d ' ' -f5 | cut -d '=' -f2 | base64 -d | grep THM{
```

![Screenshot (166)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/f0a205f3-f3ed-4f80-a06e-db49f22f95b1)

