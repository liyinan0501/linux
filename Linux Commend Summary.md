# Linux - Basic Commend

```bash
# 快速启动终端
ctr + alt + t

# 终端字体放大
ctr + shift + '+'
# 终端字体缩小
ctr + '-' 
```

## cd

```bash
# 切换到当前用户的主目录
cd ~
cd

# 切换到上一次目录
cd -

# 切换到上一级目录
cd ..

# 切换到当前目录
cd .
```

## ls

- -l已列表方式显示
- -h 显示单位
- -a 显示隐藏文件

合并命令：

```bash
ls -lha

# 以下命令相等
ls -la
ll
```

## mkdir rm

- -p 创建依赖

```bash
# 创建嵌套文件夹
mkdir AA/BB/CC -p

# 创建隐藏目录
mkdir .AA
```

- -i 交互提示
- -r 递归删除目录及其内容
- -f 强制删除，忽略不存在文件，无需提示。
- -d删除空目录

```bash
# 删除空目录
rmdir AA
rm -d AA

# 删除有内容目录
rm -r AA
```

## cp mv

- mv cp命令务必加 -i，否则不询问直接覆盖已有文件或文件夹。

- -v 显示拷贝描述。

```bash
# 拷贝文件
cp 1.txt AA -i

# 拷贝文件夹
cp AA BB -r -i -v 

# 移动文件到指定文件夹里
mv 1.txt AA

# mv 同一级目录下可以重命名
```

## I/O Redirection

把终端输出的内容，保存到指定文件中。

- `>` 如果有相同文件存在会覆盖原有文件内容，相当于文件操作中`w`模式
- `>>` 如果有相同文件存在会追加写入到文件末尾，相当于文件操作中`a`模式

```bash
ls > BB/info.txt
ls AA > BB/info.txt
```

## cat more

- cat more 只能查看文件，不能修改文件。

```bash
# 查看多个小文件内容
cat 1.txt 2.txt

ls /bin >> 3.txt
more 3.txt
# 下一页 f 或者 空格
# 上一页 b
# 下一行 回车

# 打开编辑模式
gedit 1.txt
```

## |

- 相当于数据的容器，可以把终端打印的数据保存这个管道里。
- 管道不能查看上一页

```bash
ls /bin | more
```

## ln -s & ln

- ln-s 创建软连接，相当于windows创建快捷方式。
- ln 创建硬链接

```bash
# 创建在同一目录下软连接，可以用相对路径。
ln -s 2.txt 2-s.txt

# 创建在不同目录下软连接，需要用绝对路径。
ln -s /home/yinanli/Desktop/AAA/2.txt ../2-s2.txt

# 创建目录的软连接
ln -s /home/yinanli/Desktop/AAA/ AAA-s
```







