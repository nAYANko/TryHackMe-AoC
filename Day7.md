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

LESS: This command lets you view the contents of a file one at a time, either line by line or page by page, it makes the reviewing of logs less overwhelming, to navigate use up/down keys to move line by line and pageUp(b)/pageDown(space) to move page by page. Exit by pressing q.

HEAD: Lets you view contents on top of a file. Executing `head access.log` lets you view the first 10 entries of the log. To specify the number of lines typr -n followed by number of lines.

TAIL: This command allows you to view the end of the file. To display the last 10 entries of the log, execute `tail access.log` on the terminal. To specify the number of lines typr -n followed by number of lines. 

WC: The wc command stands for word count. It's a command-line tool that counts the number of lines, words, and characters in a text file. Try executing wc access.log. By default, it prints the count of lines, words, and characters as shown in your terminal. Use -l to display line count.

NL: The nl command stands for number lines. It renders the contents of the file in a numbered line format.

CONTENTS OF PROXY LOG



