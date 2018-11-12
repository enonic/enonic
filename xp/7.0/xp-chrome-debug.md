# Debugging XP controllers with Chrome

## Nashorn Chrome Debugger

- Download [NCDbg](https://github.com/provegard/ncdbg) latest release: https://github.com/provegard/ncdbg/releases
- Unzip it in a local folder
- Start XP in Debug mode: `$XP/bin/server.sh debug`
- Start NCDbg connecting to port 5005:  `$NCDBG/bin/ncdbg.sh -c localhost:5005`
- NCDbg will print out a line with a URL
- Open URL in chrome: `chrome-devtools://devtools/bundled/inspector.html?experiments=true&v8only=true&ws=localhost:7778/dbg`
- Find applications code Sources tab, and start debugging
