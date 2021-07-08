# Beautifulsoup-CheatSheet

Library import
<pre>
import requests
from bs4 import BeautifulSoup
</pre>
Making Simple Requests
<pre>
r = requests.get("http://example.com/page")
</pre>
usually used when sending information to the server like submitting a form
<pre>
r = requests.post("http://example.com/page", data=dict(
    email="me@domain.com",
    password="secret_value"
))
</pre>
(usually used when making a search query or paging through results)
<pre>
r = requests.get("http://example.com/page", params=dict(
    query="web scraping",
    page=2
))
</pre>

Getting response
<pre>
print r.status_code
</pre>
Full response as text
<pre>
print r.text
</pre>
Find substring
<pre>
if "blocked" in r.text:
    print "we've been blocked"
</pre>
Find Content Type
<pre>
print r.headers.get("content-type", "unknown")
</pre>
Parsing Using BeautifulSoup
soup = BeautifulSoup(r.text, "html.parser")
Find all links
<pre>
links = soup.find_all("a")
</pre>
 <li class="search-result">...</li>
<pre>
tags = soup.find_all("li", "search-result")
</pre>
 <div id="bar">...</div>
<pre>
tag = soup.find("div", id="bar")
</pre>
Look for nested patterns of tags 
<pre>
tags = soup.find("div", id="search-results").find_all("a", "external-links")
</pre>
Look for all tags matching CSS selectors
<pre>
tags = soup.select("#search-results .external-links")
</pre>
Get a list of strings representing the inner contents of a tag
<pre>
inner_contents = soup.find("div", id="price").contents
</pre>
Return only the text contents within this tag, but ignore the text representation of other HTML tags
<pre>
nner_text = soup.find("div", id="price").text.strip()
</pre>
Convert the text that are extracting from unicode to ascii 
<pre>
inner_text = soup.find("div", id="price").text.strip().encode("utf-8")
</pre>
Using XPath Selectors
<pre>
BeautifulSoup doesn’t currently support XPath selectors,
</pre>
Writing to CSV
<pre>
import csv
...
with open("~/Desktop/output.csv", "w") as f:
    writer = csv.writer(f)

    # collected_items = [
    #   ["Product #1", "$10", "http://example.com/product-1"],
    #   ["Product #2", "$25", "http://example.com/product-2"],
    #   ...
    # ]

    for item_property_list in collected_items:
        writer.writerow(item_property_list)
import csv
...
field_names = ["Product Name", "Price", "Detail URL"]
with open("~/Desktop/output.csv", "w") as f:
    writer = csv.DictWriter(f, field_names)

    # collected_items = [
    #   {
    #       "Product Name": "Product #1",
    #       "Price": "$10",
    #       "Detail URL": "http://example.com/product-1"
    #   },
    #   ...
    # ]

    # Write a header row
    writer.writerow({x: x for x in field_names})

    for item_property_dict in collected_items:
        writer.writerow(item_property_dict)
</pre>
Writing to a SQLite Database
<pre>
import sqlite3

conn = sqlite3.connect("/tmp/output.sqlite")
cur = conn.cursor()
...
for item in collected_items:
    cur.execute("INSERT INTO scraped_data (title, price, url) values (?, ?, ?)",
        (item["title"], item["price"], item["url"])
    )
</pre>

Different Parser
<pre>
Python’s html.parser                                            BeautifulSoup(markup, "html.parser")
lxml’s HTML parser                                              BeautifulSoup(markup, "lxml")
lxml’s XML parser                                               BeautifulSoup(markup, "lxml-xml") BeautifulSoup(markup, "xml")
html5lib                                                        BeautifulSoup(markup, "html5lib")
</pre>
What is Web Scraping
<pre>
Web scraping is the technique to extract and read the data from the internet. The collected data can be saved and reused for data analytics
</pre>
Explain Web Scraping Procedure.
<pre>
There are multiple steps involved in web scraping:

Reading data (source code of the web page URL) from the website
Parsing this data based on the HTML tags
Storing or displaying desired scraped information
Scraped data is very useful in data analytics.
</pre>
What are the preferred programming languages for web scrapping?
<pre>
Python is the most preferred programming language for web scrapping.
It has many libraries to read and extract data from the internet, to parse and manipulate the data.
</pre>
What are the Python libraries you have used for web scrapping?
<pre>
Beautiful Soap and Scrappy are the two most useful Python modules for scrapping web information.
The request module is to read the data from internet web pages.
JSON library is used to dump, to read and to write the JSON formatting objects.
</pre>
What is the purpose of the request module in Python?
<pre>
The request module is used to read the data from the internet web pages.
You have to pass the URL from where you want to read the data along with the HTTP request method, 
header information like encoding method, response data format, and session cookies…

In the HTTP response, you get data from the website. Data can be in any format like string,
JSON, XML and YAML; based on data format mentioned in the request and server response.
</pre>
How to deal if your IP address is blocked by the website?
<pre>
If you are accessing any website more than a certain threshold, your IP address can be blocked by the website. 
Proxy IPs/servers can be used to access the web pages if your IP address is blocked.

Usually, data analytics companies web scraps millions of web pages. Many times their IP addresses get blocked.
To overcome this they use a VPN (Virtual Private Network). There are many VPN service providers.
</pre>
How does VPN work?
<pre>
You send a request to the VPN server. It reads the data from the website. VPN sends back the response to your IP address.
VPN hide your IP
</pre>
What is Robot.txt
<pre>
Robot.txt has instruction by following we will not be blocked and also have website structure
</pre>
Where Get Robot.txt
<pre>
Navigate to your domain, and just add "/robots.txt".
</pre>
