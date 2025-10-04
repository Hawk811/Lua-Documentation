# Table: Curl

Table for creating options in ui. This uses the imgui bindings. 

## Functions (3)

### `init()`

 returns curl_easy_init.

**Example Usage:**
```lua
local c = Curl.init()
```

### `SetOpt(CURL, opt, val)`

**Example Usage:**
```lua
local c = Curl.init()
Curl.SetOpt(c, Curl.OPT_URL, "URL") -- correct
Curl.SetOpt(c, Curl.OPT_FOLLOWLOCATION, 1) -- also works
Curl.SetOpt(c, 10023, { "X-Test: 123", "User-Agent: AtlasBot" })
Curl.SetOpt(c, Curl.OPT_USERAGENT, "AtlasBot/1.0")
```

### `Perform()`

executes function

**Example Usage:**
```lua
local c = Curl.init()
Curl.SetOpt(c, Curl.OPT_URL, "URL") -- correct
Curl.SetOpt(c, Curl.OPT_FOLLOWLOCATION, 1) -- also works
Curl.SetOpt(c, 10023, { "X-Test: 123", "User-Agent: AtlasBot" })
Curl.SetOpt(c, Curl.OPT_USERAGENT, "AtlasBot/1.0")
local result = Curl.Perform(c)
log.info("Response: " .. result)
```

```lua
Curl.OPT_URL;
Curl.OPT_FOLLOWLOCATION;
Curl.OPT_USERAGENT;
Curl.OPT_REFERER;
Curl.OPT_POSTFIELDS;
Curl.OPT_HTTPHEADER;
Curl.OPT_COOKIE;
Curl.OPT_COOKIEFILE;
Curl.OPT_COOKIEJAR;
Curl.OPT_ACCEPT_ENCODING;

 // Networking
Curl.OPT_PORT;
Curl.OPT_TIMEOUT;
Curl.OPT_CONNECTTIMEOUT;
Curl.OPT_LOW_SPEED_LIMIT;
Curl.OPT_LOW_SPEED_TIME;

 // Redirects and auth
Curl.OPT_MAXREDIRS;
Curl.OPT_HTTPAUTH;
Curl.OPT_USERNAME;
Curl.OPT_PASSWORD;

 // SSL/TLS
Curl.OPT_SSL_VERIFYPEER;
Curl.OPT_SSL_VERIFYHOST;
Curl.OPT_CAINFO;
Curl.OPT_CAPATH;

 // Proxies
Curl.OPT_PROXY;
Curl.OPT_PROXYPORT;
Curl.OPT_PROXYUSERPWD;

 // Verbosity / Debugging
Curl.OPT_VERBOSE;
Curl.OPT_NOBODY;
Curl.OPT_HEADER;
```
