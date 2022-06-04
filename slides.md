![text](md/image/pyconit.png)
### Viaggio nel mondo delle librerie python

Danilo Abbasciano

_danilo.abbasciano@par-tec.it_

-

## Who?

### Danilo Abbasciano

_Senior Cloud Engineer_

More than 15 years in managing large infrastructure,
coding in several languages but loves writing in Python.

I try to optimize the world!

-

![text](md/image/par-tec.png)

_https://www.par-tec.it_

Note:

Milano, Roma, Pistoia, Pomezia

-
## What?
Today i am going to list 25 python libraries which have been a part of
my toolbelt and should be a part of yours as well.

Note: Cosa vedremo oggi? Vi illustrerò 25 librerie che fanno parte
della mia cassetta di attrezzi e che spero entrino a far parte anche
della vostra.

Per ognuna di esse ci sara` una slide di presentazione con nome,
payoff, logo e link al sito. Vi spiegherò come funziona e vedremo dei
piccoli esempi di utilizzo.

Il ritmo sarà sostenuto perché ci sono molte cose che vorrei farvi
vedere.

-
## Why?
Note: Perché?
Perché è il talk che avrei voluto ascoltare quando iniziai a studiare
python.

Devo Ringraziare Il mio collega Roberto Polli per avermi spinto a
presentare il talk e Enrico Bianchi per avermi aiutato con le slide.

Iniziamo subito con la prima libreria

---
## click

Command Line Interface Creation Kit

https://click.palletsprojects.com

Note: Click è un package per la creazione di command line interfaces
in modo elegante e con pochissime righe di codice.

getopts macchinoso

Le sue principali caratteristiche sono:
 * supporto dei sottocomandi
 * generazione automatica dell'help
 * tutta la gestione delle opzioni:
   - default
   - tipo
   - descrizione

-
#### click: example
```python
import click

@click.command()
@click.option("--count", default=1, help="Number of greetings.")
@click.option("--name", prompt="Your name",
              help="The person to greet.")

def hello(count, name):
    "Simple program that greets NAME for a total of COUNT times."
    for _ in range(count):
        click.echo("Hello, %s!" % name)

if __name__ == '__main__':
    hello()
```
-
#### click: example
```bash
$ python hello.py --help
Usage: hello.py [OPTIONS]

  Simple program that greets NAME for a total of COUNT times.

Options:
  --count INTEGER  Number of greetings.
  --name TEXT      The person to greet.
  --help           Show this message and exit.
```
---
## arrow

better dates and times

http://arrow.readthedocs.io/en/latest/

Note:
è una libreria che offre un approccio logico e di facile utilizzo per
creare, manipolare, formattare e convertire date, orari e timestamp.
Estende il tipo datetime per colmare alcune lacune di
funzionamento. Vi aiuta a lavorare con date e orari usando meno
importazioni e codice piú pulito.

-
#### arrow: Why?

Python's standard library have near-complete date, time and timezone
functionality but don't work very well from a usability perspective:

 - Too many modules: datetime, time, calendar, dateutil, pytz and more
 - Too many types: date, time, datetime, tzinfo, timedelta, relativedelta, etc
 - Timezones and timestamp conversions are verbose
Note:
La libreria stadard ha già la gestione di data, ora e timezone ma non
funzionano molto bene dal punto di vista dell'usabilità:
 - Troppi moduli: datetime, time, calendar, dateutil, pytz e altri
 - Troppi tipi: date, time, datetime, tzinfo, timedelta, relativedelta, etc
 - La conversione tra fuiorari e timezones è verbosa
-
#### arrow: Example
```python
>>> import arrow
>>> utc = arrow.utcnow()
>>> utc
<Arrow [2022-05-11T21:23:58.970460+00:00]>

>>> utc = utc.shift(hours=-1)
>>> utc
<Arrow [2022-05-11T20:23:58.970460+00:00]>

>>> utc.to('US/Pacific')
<Arrow [2022-05-11T13:23:58.970460-07:00]>

>>> arrow.get('2013-05-11T21:23:58.970460+00:00')
<Arrow [2022-05-11T21:23:58.970460+00:00]>
```
Note:
arrow.now()
arrow.now( passando la zona )
arrow.shift() si può schiftare indietro o avanti
arrow.get() permette la creazione di un oggetto arrow a partire da una
stringa o da un timestamp

-
#### arrow: Example 2
```python
>>> local.timestamp
1368303838

>>> local.format()
'2022-05-11 13:23:58 -07:00'

>>> local.format('YYYY-MM-DD HH:mm:ss ZZ')
'2022-05-11 13:23:58 -07:00'

>>> local.humanize()
'an hour ago'

>>> local.humanize(locale='ko_kr')
'1시간 전'
```
Note:
esiste anche dehumanize, se ad esempio gli passi "2 giorni fa"
---
## colorama

Makes ANSI escape character sequences for producing colored terminal
text

![text](md/image/colorama.png)

https://pypi.org/project/colorama/
Note:
Le sequenze di caratteri di escape ANSI sono utilizzate
per produrre testo colorato e posizionare il cursore sui terminali di
Linux e Mac.

Colorama fa funzionare questa modalità anche su Windows perché
converte le sequenze ASCII con chiamate win32.

Le applicazioni esistenti che utilizzano sequenze ASCII per produrre
output colorato su Linux e Mac semplicemente invocando colorama.init()
possono funzionare anche su Windows

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
Note:
In Windows la chiamata init() filtra le sequenze di escape ANSI per
lo stdout e stderr e lo sostituisce con la chiamta Win32
equivalente. Per le altre piattaforme init() non ha nessun 
effetto.

---
## structlog

Makes logging faster, less painful, and more powerful by
adding structure to your log entries.

![text](md/image/structlog.png)

https://www.structlog.org/en/stable/

Note:
Usato in produzione dal 2013. Abbraccia tecnologie moderne come
asyncio. Flessibile.

-
#### structlog: usage
```python
>>> import structlog

>>> log = structlog.get_logger()

>>> log.msg("greeted", whom="world", more_than_a_str=[1, 2])
2016-09-17 10:13.45 greeted   more_than_a_str=[1, 2] whom='world'
```
Note:
Poiché i log sono dizionari, è possibile associare delle coppie
chiave/valore al tuo logger, queste saranno presenti in ogni
successiva stampa del log

log = log.bind(user="hynek", another_key=42)

-
#### structlog: usage
```python
>>> import structlog

>>> structlog.configure(
...     processors=[structlog.processors.JSONRenderer()]
... )

>>> structlog.get_logger().msg("hi")
{"event": "hi"}
```
Note:
Se volessi l'output in formato JSON per invialelo ad un sistema di
aggregazione di log come ELK o Graylog, devi solo dirgli di usare il
suo JSONRenderer

---
## bokeh

is an interactive visualization library that targets modern web
browsers for presentation

![text](md/image/bokeh.png)

https://bokeh.pydata.org/en/latest/
Note:
Ti aiuta a creare una grafici di ogni tipo, da quelli semplici
a dashboard piu complesse che prendono i dati in streaming.

Con Bokeh, puoi creare visualizzazioni basate su JavaScript senza
scrivere in JavaScript. 

-
#### bokeh
Its goal is to provide elegant, concise construction of versatile
graphics, and to extend this capability with high-performance
interactivity over very large or streaming datasets.

Bokeh can help anyone who would like to quickly and easily
create interactive plots, dashboards, and data applications.

Note:
Il suo obiettivo è fornire una costruzione elegante e concisa di
grafica. I grafici sono interattivi e ha alte prestazioni su set di
dati molto grandi.

Bokeh può aiutare chiunque desideri creare rapidamente e facilmente
grafici interattivi, dashboard e applicazioni dati.

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

Cross-platform lib for retrieving information on process and system
monitoring

https://github.com/giampaolo/psutil

-
#### psutil
psutil (process and system utilities) is a cross-platform library for
retrieving information on running processes and system utilization
(CPU, memory, disks, network, sensors).

It is useful mainly for system monitoring, profiling and limiting
process resources and management of running processes.

Note:
Implementa molte funzionalità offerte dagli strumenti a riga di
comando UNIX. Supporta le seguenti piattaforme:
 * Linux
 * windows
 * Mac OS
 * sistemi BSD
 * Sun Solaris
 * AIX

-
#### psutil: example
```python
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
```python
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
Note:
Hug è il modo più veloce e moderno per creare API.

-
#### hug
Design and develop your API once, then expose it however your
clients need to consume it. Be it locally, over HTTP, or through the
command line

Note:
Le API possono essere invocate sia localmente, tramite HTTP o tramite
la riga di comando.

È stato scritto per consumare risorse solo quando necessario, inoltre
è compilato con Cython per ottenere prestazioni migliori.

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
Note:
hug semplifica l'esposizione di più versioni dell'API, puoi
semplicemente specificare quale versione o intervallo di versioni
supporta un endpoint.

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
$ curl 'http://localhost:8000/happy_birthday?name=Danilo&age=39'
{"message": "Happy 39 Birthday Danilo!", "took": 0.0}
```

Note:
Usando docstrings e type annotation nel codice hug li utilizza per
generare automaticamente la documentazione delle API.

ed anche per la validazione e conversione degli argomenti.

---
## scrapy

framework for extracting the data you need from websites.
In a fast, simple, yet extensible way.

![text](md/image/scrapy.png)

https://scrapy.org/

Note:
Scrapy è un framework opensource ad alto livello di crawling e web
scraping, utilizzato per eseguire la scansione di siti Web ed estrarre
dati strutturati dalle loro pagine. Può essere utilizzato per molti
scopi, dal data mining al monitoraggio e ai test automatizzati. 

-
#### scrapy: example
```python
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

Note:
parse() è un metodo che verrà chiamato per gestire la risposta
scaricata per ciascuna delle request effettuate.

-
#### scrapy: selectors
```python
>>> from scrapy.selector import Selector
>>> from scrapy.http import HtmlResponse
```
```python
>>> body = '<html><body><span>good</span></body></html>'
>>> Selector(text=body).xpath('//span/text()').extract()
[u'good']
```
```python
>>> response = HtmlResponse(url='http://example.com', body=body)
>>> Selector(response=response).xpath('//span/text()').extract()
[u'good']
```
```python
>>> response.selector.xpath('//span/text()').extract()
[u'good']
```
Note:
Quando esegui lo scraping di pagine Web, l'attività più comune che
devi eseguire è estrarre i dati dall'HTML. Esistono diverse librerie
che fanno questo: 
 * BeautifulSoup (lento)
 * lxml

Scrapy ha un proprio meccanismo per l'estrazione dei dati chiamato
selector perché "selezionano" alcune parti del documento HTML
grazie a espressioni XPath o CSS.

---
## sh

sh is a full-fledged subprocess replacement that allows you to call
any program as if it were a function

![text](md/image/sh.png)

https://amoffat.github.io/sh/
Note:
ti consente di chiamare qualsiasi programma come fosse una funzione.

-
#### sh: example
```python
from sh import ifconfig
print(ifconfig("wlan0"))
```
```python
try:
    sh.ls("/doesnt/exist")
except sh.ErrorReturnCode_2:
    print("directory doesn't exist")
```
```python
sh.wc(sh.ls("-1"), "-l")
```
Note:

Da notare che queste non sono funzioni Python, stanno eseguendo i
comandi eseguibili sul tuo sistema proprio come fa la shell, e in
questo caso incapsula il binario in una funzione.

In questo modo, tutti i programmi sul tuo sistema sono
facilmente disponibili da Python.

sh si basa su varie chiamate di sistema Unix e funziona solo su
sistemi operativi simili a Unix: Linux, macOS, BSD ecc. Windows non è
supportato.

---
## ntfy
brings notification to your shell

![text](md/image/ntfy.png)

https://ntfy.readthedocs.io/en/latest/

Note: 
Può fornire automaticamente notifiche desktop quando comandi in
esecuzione molto lunghi terminano o può inviare notifiche push al tuo
telefono.

-
#### ntfy: example
```python
$ ntfy send test

# send a notification when the command `sleep 10` finishes
# this sends the message '"sleep 10" succeeded in 0:10 minutes'
$ ntfy done sleep 10

$ ntfy -b linux send "Linux Desktop Notifications!"
```
Note:
Attravarso dipendenze extra supporta mote cose tra cui:
 * emoticon
 * xmpp
 * telegram
 * slack
 * rocket.chat

---
## pydantic
Data validation and settings management using python type annotations

https://pydantic-docs.helpmanual.io/

Note:
Esegue la convalida dei dati e gestione delle impostazioni tramite annotazioni.

pydantic rinforza i type hints e quando fallisce la validazione stampa
errori user frinedly.

-
#### pydantic: example
```python
from datetime import datetime
from typing import List, Optional
from pydantic import BaseModel

class User(BaseModel):
    id: int
    name = 'John Doe'
    signup_ts: Optional[datetime] = None
    friends: List[int] = []

external_data = {
    'id': '123',
    'signup_ts': '2019-06-01 12:22',
    'friends': [1, 2, '3'],
}
```
-
#### pydantic: example
```python
from pydantic import ValidationError

try:
    User(signup_ts='broken', friends=[1, 2, 'not number'])
except ValidationError as e:
    print(e.json())
```
-
#### pydantic: example
```
[{
    "loc": ["id"],
    "msg": "field required",
    "type": "value_error.missing"
  },
  {
    "loc": ["signup_ts"],
    "msg": "invalid datetime format",
    "type": "value_error.datetime"
  },
  {
    "loc": ["friends", 2],
    "msg": "value is not a valid integer",
    "type": "type_error.integer"
  }
]
```
---
## networkx

for the creation, manipulation, and study of the structure, dynamics,
and functions of complex networks.

![text](md/image/networkx.svg)

https://networkx.github.io/

Note:
crea, la manipola e studia la struttura dei grafi.

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
Note:
Con NetworkX puoi caricare e salvare grafi in formati di dati
standard e non, generare molti tipi di reti, analizzarne la struttura,
costruire modelli, progettare nuovi algoritmi di rete, disegnarli e
molto altro.

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

Note:
NetworkX è usato non solo da informatici ma anche da matematici,
fisici, biologi e chi studia le scienze sociali.

---
## prompt-toolkit

building powerful interactive command lines and terminal applications

![text](md/image/prompt-toolkit.png)

https://python-prompt-toolkit.readthedocs.io
-
#### prompt-toolkit: features
 - Syntax highlighting
 - Multi-line input editing
 - Advanced code completion
 - Selecting text for copy/paste. (Both Emacs and Vi style)
 - Mouse support for cursor positioning and scrolling
 - Auto suggestions. (Like fish shell)
Note:
 * sintax highlighting
 * Multi-line input editing
 * Completamento automatico
 * Selezione del testo per copia/incolla. (Sia stile Emacs che Vi.)
 * Supporto del mouse per il posizionamento e lo scroll del
   cursore.
 * Suggerimenti automatici.
 * Ricerca avanti e indietro.
 * Funziona bene con caratteri Unicode

Funziona ovunque:
 * su sistemi Linux, OS X, OpenBSD e Windows.
 * può essere eseguita in un server telnet/ssh o in un processo
   asyncio.
-
#### prompt-toolkit: example
```python
from __future__ import unicode_literals
from prompt_toolkit import prompt

text = prompt('Give me some input: ')
print('You said: %s' % text)
```
-
#### prompt-toolkit: autocompletion example
```python
from prompt_toolkit import prompt
from prompt_toolkit.completion import WordCompleter

items = ['<html>', '<body>', '<head>', '<title>']
html_completer = WordCompleter(items)

text = prompt('Enter HTML: ', completer=html_completer)
print('You said: %s' % text)
```
-
#### prompt-toolkit: autocompletion
![text](md/image/prompt-toolkit_example.png)
---
## asciimatics

help people create simple ASCII animations on any platform

http://asciimatics.readthedocs.io
-
#### asciimatics: Why?

 - 256 colour terminals
 - Cursor positioning
 - Keyboard input (without blocking or echoing)
 - Mouse input
 - Detecting and handling when the console resizes
 - Screen scraping
Note:

 * Testo con stili e colori
 * Posizionamento del cursore
 * Input da tastiera
 * Input del mouse
 * Supporta il ridimensionamento della console
 * Screen scraping
-
#### asciimatics: Why?
In addition, it provides more complex features including:

 - Anti-aliased ASCII line-drawing
 - Image to ASCII conversion - including JPEG and GIF formats
 - Many animation effects - e.g. sprites, particle systems, banners, etc.
 - Various widgets for text UIs - e.g. buttons, text boxes, radio...

Note:
Inoltre, fornisce alcune API semplici e di alto livello per fornire
funzionalità più complesse, come:

 * Disegno di linee
 * Conversione da immagine a ASCII
 * Molti effetti di animazione
 * Vari widget per UI di testo

Attualmente è stata testata su CentOS, Raspbian, Ubuntu, Windows, OSX,
anche se dovrebbe funzionare anche per qualsiasi altra piattaforma che
fornisce un'implementazione di curses.

-
#### asciimatics: example
```python
from asciimatics.screen import Screen
from asciimatics.scene import Scene
from asciimatics.effects import Cycle, Stars
from asciimatics.renderers import FigletText

def demo(screen):
    effects = [
        Cycle(
            screen,
            FigletText("ASCIIMATICS", font='big'),
            screen.height // 2 - 8),
        Cycle(
            screen,
            FigletText("ROCKS!", font='big'),
            screen.height // 2 + 3),
        Stars(screen, (screen.width + screen.height) // 2)
    ]
    screen.play([Scene(effects, 500)])

Screen.wrapper(demo)
```
-
#### asciimatics: example
![text](md/image/asciimatics_example.png)
---
## prettytable

represent tabular data in visually appealing ASCII tables

https://pypi.org/project/PrettyTable/
-
#### prettytable: example
```python
from prettytable import PrettyTable
x = PrettyTable()

x.field_names(["City name", "Area", "Population", "Annual Rainfall"])
x.add_row(["Adelaide",1295, 1158259, 600.5])
x.add_row(["Brisbane",5905, 1857594, 1146.4])
x.add_row(["Darwin", 112, 120900, 1714.7])
x.add_row(["Hobart", 1357, 205556, 619.5])
x.add_row(["Sydney", 2058, 4336374, 1214.8])
x.add_row(["Melbourne", 1566, 3806092, 646.9])
x.add_row(["Perth", 5386, 1554769, 869.4])
```
Note:
crei un oggetto PrettyTable.
Esistono vari modi per inserire dei dati:
 * riga per riga
 * tutte le righe insieme
 * colonna per colonna
 * import da csv
 * import da database cursor
 
ed è possibile anche cancellare dati

-
#### prettytable: print(x)
```text
+-----------+------+------------+-----------------+
| City name | Area | Population | Annual Rainfall |
+-----------+------+------------+-----------------+
| Adelaide  | 1295 |  1158259   |      600.5      |
| Brisbane  | 5905 |  1857594   |      1146.4     |
| Darwin    | 112  |   120900   |      1714.7     |
| Hobart    | 1357 |   205556   |      619.5      |
| Melbourne | 1566 |  3806092   |      646.9      |
| Perth     | 5386 |  1554769   |      869.4      |
| Sydney    | 2058 |  4336374   |      1214.8     |
+-----------+------+------------+-----------------+
```
Note:

 * visualizzare la tabella...
 * visualizzare solo alcune colonne o righe
 * modificare l'ordine delle colonne
 * ordinare le righe
 * cambiare stile della tabella

---
## TheFuzz

Fuzzy string matching like a boss.

It uses Levenshtein Distance to calculate the differences between
sequences in a simple-to-use package.

https://github.com/seatgeek/thefuzz
Note:
date due stringhe calcola la distanza di Levenshtein che è la misura
di quanto le strighe sono simili.

-
#### theFuzz: example
```python
>>> from thefuzz import fuzz
>>> fuzz.ratio("fuzzy wuzzy was a bear", "wuzzy fuzzy was a bear")
    91
```
Note:
 * simle ratio
 * partial ratio
 * token sort ratio
 * ...
---
## progressbar2

A text progress bar is typically used to display the progress of a
long running operation, providing a visual cue that processing is
underway

https://progressbar-2.readthedocs.io/

Note:
Crea una barra di avanzamento testuale, viene in genere utilizzata per
visualizzare lo stato di avanzamento di un'operazione lunga,
per indicare che l'elaborazione è in corso.

Fork di un vecchio progetto progressbar non più mantenuto. È
compatibile con l'originale così si può sotituire con il nuovo
progetto senza ulteriori modifiche.

-
#### progressbar2: example
```python
import time
import progressbar

for i in progressbar.progressbar(range(100)):
    time.sleep(0.02)
```
```
19% (19 of 100) |##          | Elapsed Time: 0:00:00 ETA: 0:00:01
```
Note:
è molto facile da usare, ma molto potente.

Supporta il ridimensionamento automatico.

---
## doctest

Searches for pieces of text that look like interactive Python
sessions, and then executes those sessions to verify that they work
exactly as shown

https://docs.python.org/3/library/doctest.html

Note:
Il modulo doctest cerca parti di testo che sembrano sessioni Python
interattive, quindi li esegue per verificare che funzionino.

 * Per verificare che le docstring di un modulo siano aggiornate
   verificando che tutti gli esempi interattivi funzionino ancora come
   documentato.

 * Per eseguire test di regressione.

 * Per scrivere documentazione tutorial per un pacchetto

-
#### doctest: example
```
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
```python
import doctest
doctest.testfile("example.txt")
```

Note:
Un'altra semplice applicazione di doctest è testare gli esempi in un
file di testo.

testfile() può essere invocato anche da riga di comando. Si può usare
l'interprete Python per eseguire il modulo doctest e passargli il nome
del file:

python -m doctest -v esempio.txt

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
## pillow

friendly PIL (Python Imaging Library) fork

![text](md/image/pillow.png)

https://pillow.readthedocs.io/

Note:
ampio supporto per i formati di file

una rappresentazione interna efficiente e buona capacità di
elaborazione delle immagini.

-
#### pillow: creating thumbnails
```python
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
Note:

 * creare thumbnails
 * converte tra formati diversi
 * stampa di immagini
 * filtri
 * rotazioni
 * ridimensionamento
---
## requests-futures

Small add-on for the python requests http library.

https://github.com/ross/requests-futures

-
#### requests-futures: example
```python
from concurrent.futures import as_completed
from requests_futures.sessions import FuturesSession

futures=[session.get(f'http://httpbin.org/get?{i}') for i in range(3)]

for future in as_completed(futures):
    resp = future.result()
	print(resp.json()['url'])
```
Note:
Di default crea 8 worker.

---
## behave

uses tests written in a natural language style, backed up by Python
code

![text](md/image/behave.png)

https://behave.readthedocs.io/en/latest/
Note:
Lo sviluppo basato su behavior-driven (o BDD) è una tecnica agile di
sviluppo software che incoraggia la collaborazione tra sviluppatori,
QA e persone non tecniche.

behavior usa test scritti con un linguaggio naturale

-
#### behave: tutorial.feature
```gherkin
Feature: showing off behave

  Scenario: run a simple test
     Given we have behave installed
      When we implement a test
      Then behave will test it for us!
```
-
#### behave: tutorial.py
```python
from behave import *

@given('we have behave installed')
def step_impl(context):
    pass

@when('we implement a test')
def step_impl(context):
    assert True is not False

@then('behave will test it for us!')
def step_impl(context):
    assert context.failed is False
```
-
#### behave: run
```bash
$ behave
Feature: showing off behave # features/tutorial.feature:1

  Scenario: run a simple test        # features/tutorial.feature:3
    Given we have behave installed   # features/steps/tutorial.py:3
    When we implement a test         # features/steps/tutorial.py:7
    Then behave will test it for us! # features/steps/tutorial.py:11

1 feature passed, 0 failed, 0 skipped
1 scenario passed, 0 failed, 0 skipped
3 steps passed, 0 failed, 0 skipped, 0 undefined
```
---
## sched

implements a general purpose event scheduler

https://docs.python.org/3/library/sched.html

Note:
Il modulo Sched fa parte della libreria standard, può essere
utilizzato nella creazione di bot e altre applicazioni di monitoraggio
e automazione.

Il modulo sched implementa un programmatore di eventi generico per
l'esecuzione di attività in orari specifici.

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
## Pony

Write SQL queries using Python generators & lambdas

![text](md/image/pony.jpg)

https://ponyorm.com/

Note:
SQL ORM Object relational mapper degna alternativa a SQLAlchemy.

 * intuitivo
 * Supporta i db più popolari: SQLite, PostgreSQL, MySQL, Oracle
 * stabile

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
# Thanks
_click
arrow
colorama
structlog
bokeh
psutil
hug
scrapy
sh
ntfy
pydantic
networkx
prompt-toolkit
asciimatics
prettytable
theFuzz
progressbar2
doctest
pillow
requests-futures
behave
sched
pony_

https://github.com/piuma/pylibs-slide

__danilo.abbasciano@par-tec.it__

Note: Con questo concludo la mia presentazione
