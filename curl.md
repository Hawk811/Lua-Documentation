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
Curl.SetOpt(c, Curl.CURLOPT_URL, "https://atlasmenu.net/API/API?update_bans=0") -- correct
Curl.SetOpt(c, Curl.OPT_FOLLOWLOCATION, 1) -- also works
Curl.SetOpt(c, 10023, { "X-Test: 123", "User-Agent: AtlasBot" })
Curl.SetOpt(c, Curl.OPT_USERAGENT, "AtlasBot/1.0")
```

### `Perform()`

executes function

**Example Usage:**
```lua
local c = Curl.init()
Curl.SetOpt(c, Curl.CURLOPT_URL, "https://atlasmenu.net/API/API?update_bans=0") -- correct
Curl.SetOpt(c, Curl.OPT_FOLLOWLOCATION, 1) -- also works
Curl.SetOpt(c, 10023, { "X-Test: 123", "User-Agent: AtlasBot" })
Curl.SetOpt(c, Curl.OPT_USERAGENT, "AtlasBot/1.0")
local result = Curl.Perform(c)
log.info("Response: " .. result)
```

```lua
Curl.CURLOPT_URL;
Curl.CURLOPT_FOLLOWLOCATION;
Curl.CURLOPT_USERAGENT;
Curl.CURLOPT_REFERER;
Curl.CURLOPT_POSTFIELDS;
Curl.CURLOPT_HTTPHEADER;
Curl.CURLOPT_COOKIE;
Curl.CURLOPT_COOKIEFILE;
Curl.CURLOPT_COOKIEJAR;
Curl.CURLOPT_ACCEPT_ENCODING;

 // Networking
Curl.CURLOPT_PORT;
Curl.CURLOPT_TIMEOUT;
Curl.CURLOPT_CONNECTTIMEOUT;
Curl.CURLOPT_LOW_SPEED_LIMIT;
Curl.CURLOPT_LOW_SPEED_TIME;

 // Redirects and auth
Curl.CURLOPT_MAXREDIRS;
Curl.CURLOPT_HTTPAUTH;
Curl.CURLOPT_USERNAME;
Curl.CURLOPT_PASSWORD;

 // SSL/TLS
Curl.CURLOPT_SSL_VERIFYPEER;
Curl.CURLOPT_SSL_VERIFYHOST;
Curl.CURLOPT_CAINFO;
Curl.CURLOPT_CAPATH;

 // Proxies
Curl.CURLOPT_PROXY;
Curl.CURLOPT_PROXYPORT;
Curl.CURLOPT_PROXYUSERPWD;

 // Verbosity / Debugging
Curl.CURLOPT_VERBOSE;
Curl.CURLOPT_NOBODY;
Curl.CURLOPT_HEADER;
```
