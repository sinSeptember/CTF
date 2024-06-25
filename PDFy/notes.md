
![](https://github.com/sinSeptember/CTF/blob/main/PDFy/assets/2024-06-19_13-01.png)

# summary 
with 200OK and error in the body we were able to find a tool with vuln.
by parsing error messages and crawling the app. 
SSRF allow us manipulate the tool into accessing sensitive server-side resources.
### CHALLENGE DESCRIPTION

Welcome to PDFy, the exciting challenge where you turn your favorite web pages into portable PDF documents! It's your chance to capture, share, and preserve the best of the internet with precision and creativity. Join us and transform the way we save and cherish web content! NOTE: Leak /etc/passwd to get the flag!

notes: 
- portable pdf documents :)
-  /etc/passwd store the flag, ok ! 

# enum 
So we sent a url for a target page and the app will convert the page  into pdf format
In other words pdfy is a conversion tools.

While crawling the req/res  we can find a server header with info about the server running so I noted it:
  - Server: **Werkzeug/3.0.2 Python/3.12.2**
![](https://github.com/sinSeptember/CTF/blob/main/PDFy/assets/1.png)

The url being passed as an input so I start testing for parameter vul. for SSRF
testing with html server 
![](https://github.com/sinSeptember/CTF/blob/main/PDFy/assets/2024-06-19_12-35.png)

the response shows that our app use wkhtmltopdf to convert HTML pages to PDF.

![](https://github.com/sinSeptember/CTF/blob/main/PDFy/assets/2024-06-19_12-39.png)

# exploit
 Googling to find any valuable info about wkhtmltopdf and among many results we can found this [issue](https://github.com/wkhtmltopdf/wkhtmltopdf/issues/3570)  & [exploitation](https://exploit-notes.hdks.org/exploit/web/security-risk/wkhtmltopdf-ssrf/) that pointing to read localfile using php. 

by hosting php server on my localhost and  tunneling to the target I got the /etc/passwd reflected :) 

![](https://github.com/sinSeptember/CTF/blob/main/PDFy/assets/2024-06-19_13-00.png)


