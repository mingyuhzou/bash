# bash语法

*#!/bin/bash* 写在开头，告诉系统可以用/bin/bash来跑这个文件

**`local`** 声明局部变量，引用变量时要加上双引号

**`$1` `$2`**：函数（或脚本）的第 1、第 2 个参数。`$0` 是脚本/函数名本身，`$@` 是全部参数

**`[[ ... ]]`** 条件判断，`if 条件; then ... fi`

- `-z "$x"`：字符串是否为空（zero length）
- `-f "$x"`：这个路径是否是一个已存在的普通文件
-  `-d`目录是否存在`-n`字符串非空

循环

```bash
for g in "$@"; do                      # 遍历所有参数，每次 g 取一个
    fetch_paddlebox_log "$g" || fail=1 # 下载它；失败就把 fail 标记为 1
done
```

**`seq -w 1 14`** 生成1-14的序列，-w表示等宽补零->"01 02 ... 09 10 ... 14"

**`&&` 和 `||`**

- `A && B`：A 成功了才执行 B（逻辑与，短路）
- `A || B`：A 失败了才执行 B

**`echo ... >&2`** 打印到标准错误

**`$( ... )`** 把括号中的命令输出作为字符串

`|`把左侧的输出作为右侧的输入

`cut` 是个按列裁剪文本的小工具，三个常用选项：

- `-f`：取第几个字段（field，即第几列），`-f1` 就是第 1 列

- `-d`：指定列的分隔符（delimiter），**默认是制表符 Tab**

- ```bash
  echo "a,b,c" | cut -d',' -f1       # 输出 a    （用逗号分隔，取第1列）
  echo "a,b,c" | cut -d',' -f2       # 输出 b
  echo "a,b,c" | cut -d',' -f1,3     # 输出 a,c  （取第1和第3列）
  echo -e "x\ty" | cut -f2           # 输出 y  
  ```

格式字符串

```bash
src="${base}/${group}/stdout/paddlebox.log"
```

`du -h "$out"`  查看占用磁盘大小

`fetch_paddlebox_log() {...}`定义函数 `fetch_paddlebox_log "$@"`指定函数接受所有参数

`mkdir -p "$dst"` 建目录，-p表示父目录不存在则创建

`%/`结尾有/则删除

```bash
dst="/home/abl/"
echo "${dst%/}" 
```

