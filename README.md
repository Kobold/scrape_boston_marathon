*A quick tool to scrape the results of the 2015 Boston Marathon.*

The usual rigamarole to set up the script:

```bash
$ git clone git@github.com:Kobold/scrape_boston_marathon.git
$ cd scrape_boston_marathon
$ mkvirtualenv scrape_boston_marathon
$ pip install -r requirements.txt

$ python main.py # Show the help.
Usage: main.py [OPTIONS] COMMAND [ARGS]...

  Pile of commands to scrape the boston marathon results.

Options:
  --help  Show this message and exit.

Commands:
  output_csv   Write a csv listing of all entrants.
  output_html  Write all pages in the database into HTML...
  scrape       Pull down HTML from the server into dataset.
```

**How this thing works**

First, we have to pull down the actual results HTML. Running `python main.py
scrape` pulls down HTML and jams it into a database using the `dataset`
library. Why a database versus files? \*shrug\*

```bash
$ python main.py scrape
Requesting state 2 - page 0
Requesting state 3 - page 0
Requesting state 4 - page 0
...
```

Once the HTML is stored locally, we can do whatever we want with it—play
around with it without abusing anyone's server.

**Output tools**

`python main.py output_html` - A basic example of just dumping all the HTML in
the database to HTML files.

`python main.py output_csv` - A more substantial tool that will scrape all the
HTML in the database using BeautifulSoup, then output a csv listing the scraped
entrants to whatever filename you specify. It may take a few seconds to run
because BeautifulSoup is slow with the html5lib parser.

```bash
$ python main.py output_csv entrants.csv
Wrote 821 entrants.
```
