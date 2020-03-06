---
layout: post
title: bash常用命令
category: tech
guid: AEC029CB-72E7-4F09-A491-334348AAF79F
tags: [tech, bash]

---
{% include JB/setup %}

## String

- [判断变量内容是否为空](https://www.cyberciti.biz/faq/unix-linux-bash-script-check-if-variable-is-empty/)

```bash
local var=""

if [ -z "$var" ]; then
  echo "\$var is empty"
else
  echo "\$var is NOT empty"
fi
```

- [判断变量是否不空](https://stackoverflow.com/questions/3601515/how-to-check-if-a-variable-is-set-in-bash)

```bash
if [ -n "$1" ]; then
  echo "You supplied the first parameter!"
else
  echo "First parameter not supplied."
fi
```

可以使用非运算符-`!`, 如
```bash
if [[ ! -z "$var" ]]; then
  echo "\$var is NOT empty"
fi
```

## File

- 判断文件是否存在

```bash
if [[ -f "$file" ]]; then
  echo "File - $file exists"
else
  echo "File - $file does not exist"
fi
```

- [判断文件是否为符号链接(symbolic link)](https://linuxize.com/post/bash-check-if-file-exists/)

```bash
if [[ -L "$file" ]]; then
  echo "File - $file is symbolic link"
fi
```

读取符号链接所对应的真实文件名

```bash
local _uname="$(uname -s)"

if [[ "${_uname}" == "Darwin" ]]
then
    filepath="$(greadlink -f "$FILE")"
else
    filepath="$(readlink -f "$FILE")"
fi
```

## Directory

- [判断目录是否存在](https://linuxize.com/post/bash-check-if-file-exists/)
```bash
FILE=/etc/docker
if [ -d "$FILE" ]; then
  echo "$FILE is a directory"
fi
```

- 级联创建目录仅当其不存在的情况下
```bash
mkdir -p [/path/to/my/dir]
```

## Array
TODO
