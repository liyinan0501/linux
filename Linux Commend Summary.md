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

## cat more gedit

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
  - 把原文件删除，软连接失效。
  - 终端命令`ll`展示下，硬链接数目不会加一。

- ln 创建硬链接，相当于创建一个文件的另一个别名，主要目的是备份文件。之前的文件丢失，别名文件继续可以访问之前的数据。
  - 把原文件删除，硬链接照常工作。
  - 和单纯的复制粘贴做备份不一样的是，硬链接是同步更新的。
  - 终端命令`ll`展示下，硬链接数目加一，同样删除硬链接或者原文件其中之一的话，硬链接数目减一。


```bash
# 创建在同一目录下软连接，可以用相对路径。
ln -s 2.txt 2-s.txt

# 创建在不同目录下软连接，需要用绝对路径。
ln -s /home/yinanli/Desktop/AAA/2.txt ../2-s2.txt

# 创建目录的软连接
ln -s /home/yinanli/Desktop/AAA/ AAA-s

# 创建在同一目录下硬链接，可以用相对路径。
ln 3.txt 3-h.txt

# 创建在不同目录下硬连接，也可以用相对路径，没有必要使用绝对路径。
ln info.txt ../info-h.txt
```

- 目录可以创建软连接，目录不可以创建硬链接。

## grep

文本搜索命令

- -i 忽略大小写
- -n 显示行号
- -v 显示不包含匹配文本的所有行

```bash
# 在1.txt文件指定字符
grep ‘yinan’ 1.txt

# 搜索时忽略大小写
grep -i 'Yinan' 1.txt

-vn
```

- 可以结合正则表达式
  - ^ 以指定字符开头
  - $ 以指定字符结尾
  - . 匹配一个非换行符的字符

```bash
# 在指定文件，搜索以y开头的行并忽略大小写。
grep '^y' 1.txt -i

# 在指定文件，搜索以a结尾的行并忽略大小写。
grep 'a$' 1.txt -i

grep 'n.n' 1.txt

# 结合管道使用
ls /bin | grep 'sh'
```

- 引号可以省略

```bash
ls /bin | grep sh
```

## find

查找文件命令

- -name 根据文件名（包括文件夹名）字查找
- *代表0个或者多个任意字符
- ？代表任意一个字符
- 需要加双引号

```bash
# 在当前目录进行名字搜索
find . -name '*.txt'

# 在上目录进行名字搜索
find .. -name '*.txt'

find . -name '1*.txt'

# 不需要加双引号
rm 1*.txt
ls 1*.txt
mv *.txt CC
```

## tar zip unzip

能够使用tar命令完成文件的压缩和解压缩。

尽量使用gz格式，因为占用空间较少。

- .gz 和.bz2的压缩包需要使用tar命令来压缩和解压缩。
- .zip的压缩包需要使用zip命令来压缩，使用unzip命令来解压缩。
- -c 创建打包文件
- -v 显示包里的文件信息
- -f 指定压缩文件的文件名，必须放到所有选项后面
- -z 压缩和解压缩.gz
- -j 压缩和解压缩.bz2
- -x 解包
- -C 解压缩到指定目录
- 压缩包固定写法是 xxx.tar.gz

```bash
# 压缩 .gz
tar -zcvf test.tar.gz *.txt

# 解压 .gz 到同一目录
tar -zxvf test.tar.gz

# 解压 .gz 到指定目录 
tar -zxvf test.tar.gz -C AA

# 压缩 .bz2
tar -jcvf test.bz2 *.txt

# 解压 .bz2 到同一目录
tar -jxvf test.bz2

# 解压 .bz2 到指定目录 
tar -jxvf test.bz2 -C AA
```

能够使用 zip 和 unzip命令完成文件的压缩和解压缩。

- zip 压缩成 .zip文件
- unzip 解压缩 .zip格式文件
- -d 解压缩到指定目录

```bash
# 压缩成zip文件
# 不用写test.zip后缀
zip test *.txt

# 解压zip文件到同一目录
unzip test.zip

# 解压zip文件到指定目录
unzip test.zip -d AA
```

## chmod

能够修改文件权限

修改文件权限两种方式：

- 字母法

  角色说明

  | 角色 | 说明            |
  | ---- | --------------- |
  | u    | user 文件拥有者 |
  | g    | group 用户组    |
  | o    | other 其他用户  |
  | a    | all 所有用户    |

  权限设置：

  | 操作符 | 说明     |
  | ------ | -------- |
  | +      | 增加权限 |
  | -      | 撤销权限 |
  | =      | 设置权限 |

  权限说明：

  | 权限 | 说明       |
  | ---- | ---------- |
  | r    | 可读       |
  | w    | 可写       |
  | x    | 可执行     |
  | -    | 无任何权限 |

  ```bash
  # 修改1.txt文件所有者无读取的权限
  chmod u-r 1.txt
  cat 1.txt
  # Permission denied
  # 撤销
  chomod u+r 1.txt
  
  # 所有权限更改
  chmod a=rw 1.txt
  chmod a=- 1.txt
  
  # 分别修改权限
  chmod u=rw,g=r,o=r 1.txt
  ```

## 

- 数字法

  多种权限数字相加

  | 权限 | 说明     |
  | ---- | -------- |
  | r    | 可读 4   |
  | w    | 可写 2   |
  | x    | 可执行 1 |
  | -    | 无权限 0 |

  ```bash
  # 当前用户可读可写，同组用户可读，其他用户可读。
  chmod 644 1.txt
  -rw-r--r-- 1.txt
  
  # 所有用户可读可写可执行
  chomod 777 1.txt
  
  # 所有用户无任何权限
  chomod 000 1.txt
  ```

  



