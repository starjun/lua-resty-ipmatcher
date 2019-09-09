# lua-resty-ip-matcher

High performance match IP address for OpenResty Lua.

## API


```lua
local ip = require("resty.ipmatcher").new({
    "127.0.0.1",
    "192.168.0.0/16",
    "::1",
    "fe80::/32",
})

ngx.say(ip.match("127.0.0.1"))
ngx.say(ip.match("192.168.1.100"))
ngx.say(ip.match("::1"))
```

## ipmatcher.new

`syntax: ok, err = ipmatcher.new(ips)`

The `ips` is a array table, like `{ip1, ip2, ip3, ...}`, Each element in the array is a IP address string.

```lua
local ip, err = ipmatcher:new({"127.0.0.1", "192.168.0.0/16"})
```

Returns `nil` and error message if failed to create new `ipmatcher` instance.

It supports any CIDR format for IPv4 and IPv6.

```lua
local ip, err = ipmatcher.new({
        "127.0.0.1", "192.168.0.0/16",
        "::1", "fe80::/16",
    })
```

## ip.match

`syntax: ok, err = ip:match(ip)`

Returns a `true` or `false` if the IP exists within any of the specified IP list.

Returns `nil` and an error message with an invalid IP.

```lua
local ok, err = ip:match("127.0.0.1")
```
