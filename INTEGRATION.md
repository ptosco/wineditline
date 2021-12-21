### CMake

This project can be integrated into another project using FetchContent:
    
```CMake
FetchContent_Declare(
        WINEDITLINE
        GIT_REPOSITORY "https://github.com/ptosco/wineditline"
        GIT_TAG WinEditLine-2.207
)

FetchContent_MakeAvailable(WINEDITLINE)
```

This will make the targets `edit` and `edit_static` available. They should be populated with all the required properties to be linked with as is.

```CMake
target_link_libraries(Foo edit_static)
```

On Windows, linking with `edit` will allow the target to use the `$<TARGET_RUNTIME_DLL:Foo>` generator expression to facilitate the deployment of the target.


TODO: Add support for exporting targets to relocatable package.