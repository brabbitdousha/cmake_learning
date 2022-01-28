### configure_file
***
```
configure_file(<input> <output>
               [COPYONLY] [ESCAPE_QUOTES] [@ONLY]
               [NEWLINE_STYLE [UNIX|DOS|WIN32|LF|CRLF] ])
```
```
COPYONLY 
仅拷贝 <input> 文件里面的内容到 <output> 文件， 不进行变量的替换；
```
```
ESCAPE_QUOTES
使用反斜杠（C语言风格）来进行转义；
```
```
@ONLY

限制替换， 仅仅替换 @VAR@ 变量， 不替换 ${VAR} 变量
```
```
NEWLINE_STYLE

指定输入文件的新行格式， 例如：Unix 中使用的是 \n, windows 中使用的 \r\n
```

> COPYONLY 和 NEWLINE_STYLE 是冲突的，不能同时使用；

- example
```cpp
   configure_file (
  "${PROJECT_SOURCE_DIR}/Config.h.in"
  "${PROJECT_BINARY_DIR}/Config.h"
  )
```

### for Visual Studio
***
```
Add_Definitions(-DNOMINMAX)
对应
右键项目属性-> C/C++ -> 预处理器 -> 预处理器定义

```
```
#  %PATH%为系统环境变量的PATH
set(MY_PATH "PATH=${USD_LIBRARY_DIRECTORY};%PATH%")
set_target_properties(run_it PROPERTIES VS_DEBUGGER_ENVIRONMENT "${MY_PATH}")

对应
右键项目属性->配置属性->调试->环境

```