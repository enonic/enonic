# Debugging XP controllers with Chrome

- Download NCDbg latest release: https://github.com/provegard/ncdbg/releases
- Unzip in a folder
- Start XP in Debug mode: <xp> bin/server.sh debug
- Start NCDbg connecting to port 5005: <ncdbg> ./bin/ncdbg.sh  -c localhost:5005
- NCDbg will print out a line with a URL
Open this URL in Chrome: chrome-devtools://devtools/bundled/inspector.html?experiments=true&v8only=true&ws=localhost:7778/dbg
- Open URL in chrome: chrome-devtools://devtools/bundled/inspector.html?experiments=true&v8only=true&ws=localhost:7778/dbg
- Find applications code Sources tab and start debugging

