## Lua
### Fetch Environment Variable in lua

```lua
local my_val = os.getenv("MY_VAR_NAME") or "default"
```

```lua
debug.getinfo(1, "S").source
```

```lua
debug.getinfo(1, "S").source:match("@?(.*/)") or "./"
```

### Package.path 
- Bad: influences system environment
```lua
local root = debug.getinfo(1, "S").source:match("@?(.*/)") or "./"
package.path = root .. "src/?.lua;"
            .. root .. "src/?/init.lua;"
            .. root .. "vendor/?.lua;"
            .. root .. "vendor/?/init.lua;"
            .. package.path
```

### shell helper
```dash
#!/usr/bin/env bash
PROJECT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
export LUA_PATH="$PROJECT_DIR/src/?.lua;$PROJECT_DIR/src/?/init.lua;;"
lua "$PROJECT_DIR/src/main.lua" "$@"
```
