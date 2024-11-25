# Working with Web Services

## Overview
This project demonstrates the setup and utilization of web services using Apache, cURL, wget, and Python 3. It provides practical insights into web server configuration, data transfer, and communication testing.

---

## Apache Web Server

### Description
Apache is a widely used web server capable of dynamic webpage creation and HTTP header manipulation using various modules.

### Installation
To install Apache on a Linux system, use the following command:
```
apt install apache2 -y
```

### Example Output
```
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Suggested packages:
  apache2-doc apache2-suexec-pristine | apache2-suexec-custom
The following NEW packages will be installed:
  apache2
0 upgraded, 1 newly installed, 0 to remove and 17 not upgraded.
Need to get 95.1 kB of archives.
...
```

### Access Default Page
After starting the Apache server, navigate to http://localhost in your browser to confirm successful installation.

---

## cURL

### Description
cURL is a command-line tool for transferring data over protocols like HTTP and FTP, enabling remote testing of websites.

### Usage
```
curl http://localhost
```

### Example Output
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Apache2 Ubuntu Default Page: It works</title>
  </head>
</html>
```

---

## Wget

### Description
wget is another tool for downloading files via FTP or HTTP. It downloads and stores the website content locally.

### Usage
```
wget http://localhost
```

### Example Output
```
--2020-05-15 17:43:52--  http://localhost/
Resolving localhost (localhost)... 127.0.0.1
Connecting to localhost (localhost)|127.0.0.1|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10918 (11K) [text/html]
Saving to: 'index.html'
```

---

## Python 3 Web Server

### Description
Python 3 provides a simple way to set up a web server using its built-in HTTP server module.

### Usage
Navigate to the directory containing your web content and run:
```
python3 -m http.server
```

### Example Output
```
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
127.0.0.1 - - [15/May/2020 17:56:29] "GET /readme.html HTTP/1.1" 200 -
```

### Browser Access
Open http://localhost:8000 in your browser to view the hosted content.

---

## Key Features Covered
- Apache Web Server Setup: Installation and accessing the default web page.
- cURL: Fetching website content and analyzing HTTP communication.
- Wget: Downloading and saving web content locally.
- Python 3 HTTP Server: Hosting and testing a web server.

---

## Conclusion
This guide covers fundamental operations for working with web services. These tools and techniques serve as a foundation for managing and testing web servers effectively.
