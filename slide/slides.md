# PyRoma
### 20 librerie python di cui non potrai fare a meno

Danilo Abbasciano

danilo@piumalab.org
-
## Who?
```python
def my(self):
    """
    Senior System Engineer.

    Managing large infrastructure,
    coding in several languages but loves writing in Python.

    I try to optimize the world!
    """
    pass
```
-
## What?
Today i am going to list 20 python libraries which have been a part of
my toolbelt and should be a part of yours as well.
-
## Why?

---
## arrow
better dates and times

http://arrow.readthedocs.io/en/latest/
-
#### arrow: Why?
Python's standard library have near-complete date, time and timezone
functionality but don't work very well from a usability perspective:

 - Too many modules: datetime, time, calendar, dateutil, pytz and more
 - Too many types: date, time, datetime, tzinfo, timedelta, relativedelta, etc.
 - Timezones and timestamp conversions are verbose
-
#### arrow: Example
```python
>>> import arrow
>>> utc = arrow.utcnow()
>>> utc
<Arrow [2013-05-11T21:23:58.970460+00:00]>

>>> utc = utc.shift(hours=-1)
>>> utc
<Arrow [2013-05-11T20:23:58.970460+00:00]>

>>> local = utc.to('US/Pacific')
>>> local
<Arrow [2013-05-11T13:23:58.970460-07:00]>

>>> arrow.get('2013-05-11T21:23:58.970460+00:00')
<Arrow [2013-05-11T21:23:58.970460+00:00]>
```
-
#### arrow: Example 2
```python
>>> local.timestamp
1368303838

>>> local.format()
'2013-05-11 13:23:58 -07:00'

>>> local.format('YYYY-MM-DD HH:mm:ss ZZ')
'2013-05-11 13:23:58 -07:00'

>>> local.humanize()
'an hour ago'

>>> local.humanize(locale='ko_kr')
'1시간 전'
```
---
## Pony

Write SQL queries using Python generators & lambdas

![text](md/image/pony.jpg)

https://ponyorm.com/
-
#### pony: example
```python
select(c for c in Customer if sum(c.orders.price) > 1000)
```
```sql
SELECT "c"."id"
FROM "customer" "c"
  LEFT JOIN "order" "order-1"
    ON "c"."id" = "order-1"."customer"
GROUP BY "c"."id"
HAVING coalesce(SUM("order-1"."total_price"), 0) > 1000
```
-
#### pony: example 2
```python
select(c for c in Customer if sum(c.orders.price) > 1000)
```
Here is the same query written using the lambda function:
```python
Customer.select(lambda c: sum(c.orders.price) > 1000)
```
---
## colorama
Makes ANSI escape character sequences for producing colored terminal
text

![text](md/image/colorama.png)

https://pypi.org/project/colorama/
-
#### colorama: example
```python
from colorama import init, Fore, Back, Style
init()

print(Fore.RED + 'some red text')
print(Back.GREEN + 'and with a green background')
print(Style.DIM + 'and in dim text')
print(Style.RESET_ALL)
print('back to normal now')
```
---
## colorlog
Log formatting with colors

![text](md/image/colorlog.png)

https://pypi.org/project/colorlog/
-
#### colorlog: usage
```
import colorlog

handler = colorlog.StreamHandler()
handler.setFormatter(colorlog.ColoredFormatter(
	'%(log_color)s%(levelname)s:%(name)s:%(message)s'))

logger = colorlog.getLogger('example')
logger.addHandler(handler)
```
---
## begins

Command line programs for lazy humans

https://pypi.org/project/begins/
-
#### begins: example
```python
import begin

@begin.start
def run(name='Arther', quest='Holy Grail', colour='red', *knights):
    "tis but a scratch!"
```
-
#### begins: example
```bash
usage: example.py [-h] [-n NAME] [-q QUEST] [-c COLOUR]
                  [knights [knights ...]]

tis but a scratch!

positional arguments:
  knights

optional arguments:
  -h, --help            show this help message and exit
  -n NAME, --name NAME  (default: Arther)
  -q QUEST, --quest QUEST
                        (default: Holy Grail)
  -c COLOUR, --colour COLOUR
                        (default: red)
```
---
## pywebview

lightweight cross-platform wrapper around webview

![text](md/image/pywebview.png)

https://github.com/r0x0r/pywebview
-
#### pywebview
allows to display HTML content in its own native GUI
window.

It gives you power of web technologies in your desktop
application, hiding the fact that GUI is browser based.
-
![text](md/image/pywebview_example.png)
---
## bokeh
is an interactive visualization library that targets modern web
browsers for presentation

![text](md/image/bokeh.png)

https://bokeh.pydata.org/en/latest/
-
#### bokeh
Its goal is to provide elegant, concise
construction of versatile graphics, and to extend this capability with
high-performance interactivity over very large or streaming
datasets.

Bokeh can help anyone who would like to quickly and easily
create interactive plots, dashboards, and data applications.
-
#### bokeh: example
```python
from __future__ import division
import numpy as np
from bokeh.plotting import figure, show, output_file

N = 20
img = np.empty((N,N), dtype=np.uint32)
view = img.view(dtype=np.uint8).reshape((N, N, 4))
for i in range(N):
    for j in range(N):
        view[i, j, 0] = int(i/N*255)
        view[i, j, 1] = 158
        view[i, j, 2] = int(j/N*255)
        view[i, j, 3] = 255

p = figure(x_range=(0,10), y_range=(0,10))

# must give a vector of images
p.image_rgba(image=[img], x=0, y=0, dw=10, dh=10)

output_file("image_rgba.html", title="image_rgba.py example")

show(p) # open a browser
```
-
#### boke: output
![text](md/image/bokeh_example.png)
---
## psutil

Cross-platform lib for process and system monitoring

https://github.com/giampaolo/psutil
-
#### psutil
psutil (process and system utilities) is a cross-platform library for
retrieving information on running processes and system utilization
(CPU, memory, disks, network, sensors).

It is useful mainly for system monitoring, profiling and limiting
process resources and management of running processes.
-
#### psutil: example
```
>>> import psutil
>>> psutil.cpu_count()
4
>>> for x in range(3):
...     psutil.cpu_percent(interval=1, percpu=True)
...
[4.0, 6.9, 3.7, 9.2]
[7.0, 8.5, 2.4, 2.1]
[1.2, 9.0, 9.9, 7.2]
```
-
#### psutil: example
```
>>> psutil.disk_usage('/')
sdiskusage(total=52576092160, used=44855128064, free=5019832320, percent=89.9)

>>> psutil.users()
[suser(name='giampaolo', terminal='pts/2', host='localhost', started=1524468091.0, pid=1352),
 suser(name='piuma', terminal='tty2', host='/dev/tty2', started=1524468096.0, pid=1375)]
```
---
## hug

Drastically simplify API development over multiple interfaces

![text](md/image/hug.png)

http://www.hug.rest/
-
#### hug
Design and develop your API once, then expose it however your
clients need to consume it. Be it locally, over HTTP, or through the
command line
-
#### hug: example
```python
import hug

@hug.get(examples='name=Timothy&age=26')
@hug.local()
def happy_birthday(name: hug.types.text, age: hug.types.number, hug_timer=3):
    """Says happy birthday to a user"""
    return {'message': 'Happy {0} Birthday {1}!'.format(age, name), 'took': float(hug_timer)}
```
```bash
$ hug -f example.py
```
-
#### hug: response
```bash
$ curl 'http://localhost:8000/happy_birthday'
{"errors":
  {
    "name": "Required parameter 'name' not supplied",
     "age": "Required parameter 'age' not supplied"
  }
}
```
```bash
$ curl 'http://localhost:8000/happy_birthday?name=Danilo&age=32'
{"message": "Happy 32 Birthday Danilo!", "took": 0.0}
```
---
## scrapy

framework for extracting the data you need from websites.
In a fast, simple, yet extensible way.

![text](md/image/scrapy.png)

https://scrapy.org/
-
#### scrapy: example
```
import scrapy

class BlogSpider(scrapy.Spider):
    name = 'blogspider'
    start_urls = ['https://blog.scrapinghub.com']

    def parse(self, response):
        for title in response.css('h2.entry-title'):
            yield {'title': title.css('a ::text').extract_first()}

        for next_page in response.css('div.prev-post > a'):
            yield response.follow(next_page, self.parse)
```
-
#### scrapy: selectors
```
>>> from scrapy.selector import Selector
>>> from scrapy.http import HtmlResponse
```
```
>>> body = '<html><body><span>good</span></body></html>'
>>> Selector(text=body).xpath('//span/text()').extract()
[u'good']
```
```
>>> response = HtmlResponse(url='http://example.com', body=body)
>>> Selector(response=response).xpath('//span/text()').extract()
[u'good']
```
```
>>> response.selector.xpath('//span/text()').extract()
[u'good']
```
---
## pysftpserver

pysftpserver An OpenSSH SFTP wrapper

https://github.com/unbit/pysftpserver
-
#### pysftpserver: Features

 * Possibility to automatically jail users in a virtual chroot environment as soon as they login
 * Possibility to automatically forward SFTP requests to another server
 * Compatible with both Python 2 and Python 3
 * Fully extensible and customizable (examples below)
 * Totally conforms to the SFTP RFC
---
## lxml

it's the most feature-rich and easy-to-use library for processing XML
and HTML

![text](md/image/lxml.png)

http://lxml.de/

-
#### lxml: Why?

 * Pythonic API
 * Documented
 * Use Python unicode strings in API
 * Safe (no segfaults)
 * No manual memory management
---
## jsonschema

an implementation of JSON Schema

https://python-jsonschema.readthedocs.io
-
#### jsonschema: example
```python
>>> from jsonschema import validate

>>> # A sample schema, like what we'd get from json.load()
>>> schema = {
...     "type" : "object",
...     "properties" : {
...         "price" : {"type" : "number"},
...         "name" : {"type" : "string"},
...     },
... }

>>> # If no exception is raised the instance is valid.
>>> validate({"name" : "Eggs", "price" : 34.99}, schema)
```
-
#### jsonschema: example
```python
>>> from jsonschema import validate

>>> # A sample schema, like what we'd get from json.load()
>>> schema = {
...     "type" : "object",
...     "properties" : {
...         "price" : {"type" : "number"},
...         "name" : {"type" : "string"},
...     },
... }

>>> validate({"name" : "Eggs", "price" : "Invalid"}, schema)
Traceback (most recent call last):
    ...
ValidationError: 'Invalid' is not of type 'number'
```
---
## networkx

for the creation, manipulation, and study of the structure, dynamics,
and functions of complex networks.

![text](md/image/networkx.png)

https://networkx.github.io/
-
#### networkx: example
```python
>>> import networkx as nx
>>> G = nx.Graph()

>>> G.add_node(1)
>>> G.add_nodes_from([2, 3])

>>> G.add_edge(1, 2)
>>> G.add_edges_from([(1, 2), (1, 3)])
```
-
#### networkx: example
```python
import matplotlib.pyplot as plt
import networkx as nx

G = nx.star_graph(20)
pos = nx.spring_layout(G)
colors = range(20)
nx.draw(G, pos, node_color='#A0CBE2', edge_color=colors,
        width=4, edge_cmap=plt.cm.Blues, with_labels=False)
plt.show()
```
-
#### networkx: example
![text](md/image/networkx_example.png)
---
## prompt-toolkit
---
## asciimatics

help people create simple ASCII animations on any platform

http://asciimatics.readthedocs.io
-
#### asciimatics: Why?

 - tyled text - including 256 colour terminals
 - Cursor positioning
 - Keyboard input (without blocking or echoing)
 - Mouse input (terminal permitting)
 - Detecting and handling when the console resizes
 - Screen scraping

In addition, it provides some simple, high-level APIs to provide more complex features including:

 - Anti-aliased ASCII line-drawing
 - Image to ASCII conversion - including JPEG and GIF formats
 - Many animation effects - e.g. sprites, particle systems, banners, etc.
 - Various widgets for text UIs - e.g. buttons, text boxes, radio
 - buttons, etc.
-

---
## prettytable
---
## wget
---
## snowballstemmer
---
## sh
---
## fuzzywuzzy
---
## progressbar
---
## doctest

searches for pieces of text that look like interactive Python
sessions, and then executes those sessions to verify that they work
exactly as shown

https://docs.python.org/2/library/doctest.html
-
#### doctest: example
```python
import doctest
doctest.testfile("example.txt")
```
```python
The ``example`` module
======================

Using ``factorial``
-------------------

This is an example text file in reStructuredText format.
First import ``factorial`` from the ``example`` module:

    >>> from example import factorial

Now use it:

    >>> factorial(6)
    120
```
-
#### doctest: example
```
File "./example.txt", line 14, in example.txt
Failed example:
    factorial(6)
Expected:
    120
Got:
    720
```
---
## nose

nose extends unittest to make testing easier

http://nose.readthedocs.io/
---
## pillow

friendly PIL (Python Imaging Library) fork

https://pillow.readthedocs.io/
-
#### pillow: creating thumbnails
```
from PIL import Image

size = (128, 128)

try:
    im =  Image.open("Image.png")
except:
    print "Unable to load image"

im.thumbnail(size)
im.save("image.jpeg")
im.show()
```
---
## pytest-play

is a pytest plugin that let you play a json file
containing previously recorded selenium splinter actions driving your
browser for your UI test.

https://github.com/davidemoro/pytest-play
---
## grequests

GRequests allows you to use Requests with Gevent to make asynchronous
HTTP Requests easily

https://github.com/kennethreitz/grequests
-
#### grequests
```
import grequests
urls = [
    'http://www.piumalab.org',
    'http://kernel.org',
    'http://python-requests.org',
    'http://fakedomain/'
]
# Create a set of unsent Requests:
rs = (grequests.get(u) for u in urls)

# Send them all at the same time:
grequests.map(rs)
```
---
## sched

implements a general purpose event scheduler

https://docs.python.org/3/library/sched.html
-
#### sched: example
```python
>>> import sched, time
>>> s = sched.scheduler(time.time, time.sleep)
>>> def print_time(a='default'):
...     print("From print_time", time.time(), a)
...
>>> def print_some_times():
...     print(time.time())
...     s.enter(10, 1, print_time)
...     s.enter(5, 2, print_time, argument=('positional',))
...     s.enter(5, 1, print_time, kwargs={'a': 'keyword'})
...     s.run()
...
>>> print_some_times()
930343690.257
From print_time 930343695.274 positional
From print_time 930343695.275 keyword
From print_time 930343700.273 default
```
---
# Thanks

#### danilo@piumalab.org

https://github.com/piuma/pylibs-slide
