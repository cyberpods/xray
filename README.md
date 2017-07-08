# XRAY

XRay is a tool for network OSINT gathering, its goal is to make some of the initial tasks of information gathering and network mapping automatic.

![xray](https://pbs.twimg.com/media/DEOZt1bWsAEOsMX.jpg)

## Notes

**Shodan API Key**

The [shodan.io](https://www.shodan.io/) API key parameter ( `-shodan-key KEY` ) is optional, however if not specified, no service fingerprinting will be performed and a lot less information will be shown (basically it just gonna be DNS subdomain enumeration).

**Anonymity and Legal Issues**

The software will rely on your main DNS resolver in order to enumerate subdomains, also, several TCP connections might be directly established from your host to the computers of the network you're scanning in order to grab banners from open ports. Technically, you're just connecting to public addresses with open ports (and **there's no port scanning involved**, as such information is grabbed indirectly using Shodan API), but you know, someone might not like such behaviour.

If I were you, I'd find a way to proxify the whole process ... #justsaying

## Installation

    go get github.com/evilsocket/xray
    cd $GOPATH/src/github.com/evilsocket/xray/
    make get_glide
    make install_dependencies
    make build

You'll find the executable in the `build` folder.

## Usage

    Usage: xray -shodan-key YOUR_SHODAN_API_KEY -domain TARGET_DOMAIN
    Options:
      -address string
            IP address to bind the web ui server to. (default "127.0.0.1")
      -consumers int
            Number of concurrent consumers. (default 16)
      -domain string
            Base domain to start enumeration from.
      -port int
            TCP port to bind the web ui server to. (default 8080)
      -session string
            Session file name. (default "<domain-name>-session.json")
      -shodan-key string
            Shodan API key.
      -wordlist string
            Wordlist file to use for enumeration. (default "wordlists/default.lst")

Example:

    xray -shodan-key yadayadayadapicaboo... -domain fbi.gov

## TODO

Session support is not complete: once session is restored, DNS bruteforcing should start from last line.

## License

This project is copyleft of [Simone Margaritelli](https://www.evilsocket.net/) and released under the GPL 3 license.

The files in the `wordlists` folder have been taken from various open source tools accross several weeks and I don't remember all of them. If you find the wordlist of your project here and want to be mentioned, feel free to open an issue or send a pull request.