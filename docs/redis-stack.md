# Support for redis-stack

## RedisJson support

Currently, Redis Json module is fully implemented (see [supported commands](./redis-commands/RedisJson/)).
Support for JSON commands (e.g., [`JSON.GET`](https://redis.io/commands/json.get/)) is implemented using
[jsonpath-ng,](https://github.com/h2non/jsonpath-ng) you can simply install it using `pip install 'fakeredis[json]'`.

```pycon
>>> import fakeredis
>>> from redis.commands.json.path import Path
>>> r = fakeredis.FakeStrictRedis()
>>> assert r.json().set("foo", Path.root_path(), {"x": "bar"}, ) == 1
>>> r.json().get("foo")
{'x': 'bar'}
>>> r.json().get("foo", Path("x"))
'bar'
```

## Lua support

If you wish to have Lua scripting support (this includes features like ``redis.lock.Lock``, which are implemented in
Lua), you will need [lupa](https://pypi.org/project/lupa/), you can simply install it
using `pip install 'fakeredis[lua]'`
