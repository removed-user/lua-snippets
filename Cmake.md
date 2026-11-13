## Cmake
### Get Binary location
```cmake
find_program(VARIABLE_NAME lua REQUIRED)
```

### Read Environment Variable in cmake
```cmake
$ENV{MY_SYSTEM_VAR}
```

### Fallback for unset environment variable
```cmake
if(NOT MY_ENV_VALUE)
    set(MY_ENV_VALUE "default_value")
endif()
```

### Set it in Cmake (BAD)
- Always prefer using fallback method
```cmake
set(MY_ENV_VALUE "$ENV{MY_VAR_NAME}")
```

### Set Build Config Output File
- Configure input file into the output file
```cmake
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/config.in"
    "${CMAKE_CURRENT_BINARY_DIR}/config"
    @ONLY
)
```

### If Statement
```cmake
if(NOT RETURN_VALUE EQUAL 0)
    message(FATAL_ERROR "script failed with exit code: ${RETURN_VALUE}")
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
