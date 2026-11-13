## Lua
### Fetch Environment Variable in lua
```lua
local my_val = os.getenv("MY_VAR_NAME") or "default"
print(my_val)
```

## Cmake
### Get Lua Interpreter
```cmake
find_program(LUA_EXECUTABLE lua REQUIRED)
```

### Read Environment Variable in cmake
```cmake
$ENV{MY_SYSTEM_VAR}
```

### Set it in Cmake
```cmake
set(MY_ENV_VALUE "$ENV{MY_VAR_NAME}")
```

### Fallback when environment variable is not set
```cmake
if(NOT MY_ENV_VALUE)
    set(MY_ENV_VALUE "default_value")
endif()
```

### Set Build Config Output File
```cmake
Configure input file into the output Lua file
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/config.lua.in"
    "${CMAKE_CURRENT_BINARY_DIR}/config.lua"
    @ONLY
)
```


