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

### If Statement
```cmake
if(NOT LUA_RES EQUAL 0)
    message(FATAL_ERROR "Lua script failed with exit code: ${LUA_RES}")
endif()
```

### Inline One-Liners at Configure Time
```cmake
execute_process(
    COMMAND ${LUA_EXECUTABLE} -e "print('Hello from Lua!')"
    OUTPUT_VARIABLE LUA_OUT
    OUTPUT_STRIP_TRAILING_WHITESPACE
)
```

