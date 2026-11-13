## Fetch Environment Variable in lua
```lua
local my_val = os.getenv("MY_VAR_NAME") or "default"
print(my_val)
```
## Fetch Environment Variable in cmake
```cmake
# 1. Read the environment variable from the system
set(MY_ENV_VALUE "$ENV{MY_VAR_NAME}")

# Optionally provide a fallback if the environment variable is not set
if(NOT MY_ENV_VALUE)
    set(MY_ENV_VALUE "default_value")
endif()
```
### Set Build Config Output File
```cmake
# 2. Configure the input file into the output Lua file
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/config.lua.in"
    "${CMAKE_CURRENT_BINARY_DIR}/config.lua"
    @ONLY
)
```


### Get Lua Interpreter
```cmake
find_program(LUA_EXECUTABLE lua REQUIRED)
```
