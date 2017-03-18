TrafficGenerator
======
This tool can be used to generate real (fake) traffic on a specific website (domain). It uses the headless browser phantomjs, so that all content will be rendered similar to a real browser, making it hardly to distinguish. 
HTTP proxy lists and random user agents are also supported. 

After visiting a page the tool will randomly select one link from the page and click on it. Only links from the same domain are visisted.

## Usage 
The usage should be quite simple. 

```
$> python2 main.py --help
usage: main.py [-h] -d DOMAIN [-s] [-f] [-t THREADS] [-to TIMEOUT]
               [-mo MAX_OFFSET] [-mac MAX_CLICKS] [-mic MIN_CLICKS]
               [-pf PROXY_FILE]

Generate traffic on a domain

optional arguments:
  -h, --help            show this help message and exit
  -d DOMAIN, --domain DOMAIN
                        The domain to generate traffic on
  -s, --secure          Use a secure connection
  -f, --forever         Run forever
  -t THREADS, --threads THREADS
                        Number of threads to use
  -to TIMEOUT, --timeout TIMEOUT
                        Request timeout in seconds
  -mo MAX_OFFSET, --max-offset MAX_OFFSET
                        Max timeout between link clicks
  -mac MAX_CLICKS, --max-clicks MAX_CLICKS
                        Max number of link clicks per thread.
  -mic MIN_CLICKS, --min-clicks MIN_CLICKS
                        Max number of link clicks per thread.
  -pf PROXY_FILE, --proxy-file PROXY_FILE
                        Path to a HTTP proxy list file. One proxy host:port
                        per line
```
For example:

```
$> python main.py  -d news.ycombinator.com --threads 10  --max-clicks 5 --min-clicks=1 --forever --proxy-file proxies.txt --timeout 60 --max-offset 10
[168.187.239.10:80] Found 195 links
[168.187.239.10:80] Visiting now: https://news.ycombinator.com/item?id=13897826
[168.187.239.10:80] Found 49 links
[168.187.239.10:80] Visiting now: https://news.ycombinator.com/user?id=grammr
[168.187.239.10:80] Found 12 links
[168.187.239.10:80] Visiting now: https://news.ycombinator.com/ask
[168.187.239.10:80] Found 165 links
[168.187.239.10:80] Visiting now: https://news.ycombinator.com/vote?id=13895140&how=up&goto=ask
[94.46.177.99:80] Found 195 links
[94.46.177.99:80] Visiting now: https://news.ycombinator.com/from?site=hackernoon.com
[94.46.177.99:80] Found 165 links
[94.46.177.99:80] Visiting now: https://news.ycombinator.com/item?id=13887634
[94.46.177.99:80] Found 21 links
[94.46.177.99:80] Visiting now: https://news.ycombinator.com/login?goto=item%3Fid%3D13887634
[94.46.177.99:80] Found 1 links
[94.46.177.99:80] Visiting now: https://news.ycombinator.com/forgot
[94.23.60.121:80] Found 195 links
[94.23.60.121:80] Visiting now: https://news.ycombinator.com/vote?id=13901950&how=up&goto=news
[94.23.60.121:80] Found 1 links
[94.23.60.121:80] Visiting now: https://news.ycombinator.com/forgot
[94.23.60.121:80] Found 0 links
[94.23.60.121:80] Visiting now: previous page
[94.23.60.121:80] Found 1 links
[94.23.60.121:80] Visiting now: https://news.ycombinator.com/forgot
[173.212.203.122:3128] Found 195 links
[173.212.203.122:3128] Visiting now: https://news.ycombinator.com/item?id=13902864
```

## Setup

Requirements:

- Python2 + Virtualenv + Pip
- NodeJS + NPM

Clone this repository:

```
git clone https://github.com/gehaxelt/python-trafficgenerator.git
cd python-trafficgenerator
```

Install phantomjs:

```
npm install phantomjs-prebuilt
```

Setup virtualenv and install dependencies:

```
virtualenv venv
. ./venv/bin/activate
pip install -r requirements.txt
```

Download and prepare a HTTP proxy list:

```
$> curl  http://txt.proxyspy.net/proxy.txt -o- | grep '+ $'| awk -F' ' '{print $1}' | sort -R > proxies.txt
```

## License

See LICENCE.md