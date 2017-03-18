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
$> python main.py  -d DOMAIN --threads 10  --max-clicks 5 --min-clicks=1 --forever --proxy-file proxies.txt --timeout 60 --max-offset 180
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