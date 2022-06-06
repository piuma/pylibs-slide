### Viaggio nel mondo delle librerie python

#### Elevator pitch

25 utili librerie in 30 minuti

#### Descrizione

Attraverso un affascinate viaggio tra le librerie python, tratteremo
rapidamente quelle più utili e semplici da utilizzare che ci faranno
risparmiare tempo e linee di codice. Farò una rapida presentazione per
ognuna di esse facendone risaltare i benefici e le principali
funzionalità. Da non perdere!

#### Libreries

 * click
 * arrow
 * colorama
 * structlog
 * bokeh
 * psutil
 * hug
 * scrapy
 * sh
 * ntfy
 * pydantic
 * networkx
 * prompt-toolkit
 * asciimatics
 * prettytable
 * theFuzz
 * progressbar2
 * doctest
 * pillow
 * requests-futures
 * behave
 * sched
 * pony

#### How to show slides

```bash
# Pull repos
git clone https://github.com/piuma/pylibs-slide.git

# Run docker container https://github.com/piuma/md-slide
docker run --rm -p 8000:8000 -p 35729:35729 \
  -v "$PWD/":/reveal.js/md piuma/md-slide
  
```
Then open browser at url http://localhost:8000

#### How to export to pdf
```bash
$ npm install decktape

$`npm bin`/decktape -s 1024x768 http://localhost:8000/ slide.pdf
```
