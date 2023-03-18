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

| 命令选项 | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| -i       | 交互式提示                                                   |
| -r       | 递归拷贝目录及内容                                           |
| -v       | 显示拷贝后的路径描述                                         |
| -a       | 保留文件或文件夹下的文件原有权限，不加这个拷贝后，原有权限会丢失。 |

```bash
# 拷贝文件
cp 1.txt AA -i

# 拷贝文件夹
cp AA BB -r -i -v 
cp AAA CCC -ria

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




## shutdown reboot

- `shutdown -h now` 立刻关键
- `reboot` 重启

## passwd

- 修改当前用户密码

## useradd

**创建用户**

- -m 自动创建用户的主目录。
- -g 指定用户所属的用户组，默认不指定会自动创建一个同名的用户组。

```bash
whoami

# 创建用户
sudo useradd -m venla

# 查看用户信息
cat /etc/passwd
cat /etc/group
id
id venla

# 创建用户密码
sudo passwd venla

# 切换用户
su - venla
whoami
```

**修改用户**

每个用户只属于一个用户组（主组），但是可以有很多个附加组。

- usermod 修改用户信息
- -G 设置一个附加组
- -g 修改用户组（主组）

```bash
# 查看附加组sudo下的用户
cat /etc/group

# 因为当前用户下没有权限设置附加组，需要exit先退出来到有权限的用户。
exit

# 给用户设置附加组
sudo usermod -G sudo venla

# 查看是否设置成功
id venla
```

**删除附加组**

- gpasswd 添加和删除附加组信息。
- -a 用户名，给用户添加附加组。
- -d用户名，给用户删除附加组。

```bash
# 把用户从附加组（sudo）中删除
sudo gpasswd -d venla sudo

# 查看是否设置成功
id venla
```

**删除用户**

- userdel 删除用户
- -r 用户名，删除用户主目录，必须要设置，否则用户主目录不会删除

```bash
# 需要退出要删除的用户，然后关闭终端。
exit

# 删除用户
sudo userdel -r venla

# 检查是否删除成功
cat /etc/passwd
cat /etc/group
```

## groupadd

**创建用户组**

- groupadd 创建用户组

```bash
sudo groupadd test

# 确认是否创建成功
ls /etc/group
```

- 创建用户并制定用户组

```bash
sudo useradd -m -g test venla

# 查看设置是否成功
grep test /etc/group
```

**修改用户组**

```bash
sudo usermod -g abc venla
```

**删除用户组**

```bash
sudo groupdel test

# 如果用户组下有用户，需要先删除用户。
sudo groupdel abc
sudo userdel -r venla
```

# Vim

**三种模式：**

- 命令模式
- 编辑模式
- 末行模式

vim打开文件默认进入的是命令模式

命令模式 > 编辑模式 输入：`i `

编辑模式 > 命令模式 输入：`esc`

命令模式 > 末行模式 输入：`：`

末行模式 > 命令模式 输入：`esc`

- `:w` 写入，不退出。
- `:wq` 或 `:x` 写入退出。
- `:q!` 强制退出，不会保存。

**vim 常用命令：**

| 命令                                          | 说明                                              |
| --------------------------------------------- | ------------------------------------------------- |
| y                                             | 复制                                              |
| yy                                            | 复制光标所在行                                    |
| p                                             | 粘贴 (粘贴5次`5p`)                                |
| dd                                            | 删除/剪切当前行                                   |
| V                                             | 按行选中，光标所经过的行都会被选中。再按G会全选。 |
| u                                             | 撤销                                              |
| ctr+r                                         | 反撤销                                            |
| >>                                            | 往右缩进                                          |
| <<                                            | 往左缩进                                          |
| :/搜索内容                                    | 搜索指定内容，下一个n，上一个N。                  |
| :%s/要替换的内容/替换后的内容/g               | 全局替换(%表示整个文件，s表示替换，g表示全局替换) |
| :开始行数,结束行数s/要替换的内容/替换后的内容 | 局部替换                                          |
| .                                             | 重复上一次命令操作                                |
| G                                             | 回到最后一行                                      |
| gg                                            | 回到第一行                                        |
| 数字+G                                        | 回到指定行                                        |
| shift+6                                       | 回到当前行的行首                                  |
| shift+4                                       | 回到当前行的行末                                  |
| ctr+f                                         | 下一屏                                            |
| ctr+b                                         | 上一屏                                            |

# Install

- 离线安装 .deb

  - 安装 `sudo dpkg -i xxxx.deb`
  - 卸载 `sudo dpkg -r xxxx`

- 在线安装 apt-get

  - 安装 `sudo apt-get install xxxx`

  - 更新下载列表 `sudo apt-get update` 告诉我们服务器有哪些软件不让下载

  - 卸载 `sudo apt-get remove xxxx`

    

# Process

进程

一个正在运行的程序或者软件就是一个进程process，只要启动一个进程，操作系统需要给这个进程分配内存资源，从而保证进程运行。

一个程序运行后至少有一个进程，一个进程默认有一个线程，进程里面可以创建多个线程，线程是衣服在进程里面，没有进程就没有线程。

例如，hello.py 程序会创建一个进程，默认提供一个线程，这个线程执行里面的代码。

- 能够使用多进程完成多任务

1. 导入进程包

   `import multiprocessing`

2. Process 进程类说明

   **Process([group [, target [, name [, args [, kwargs]]]]])**

   - group: 进程组，目前只能使用None，不用设置。
   - target: 执行的目标任务名(一个函数或一个方法)。
   - name: 进程名字，一般不会设置，会有默认名字Process-N。
   - args: 以元组方式给执行任务传参。
   - kwargs: 以字典方式给执行任务传参。

   **Process 创建的实力对象的常用方法**

   - start(): 启动子进程实例(创建子进程)。
   - join(): 等待子进程执行结束。
   - terminate(): 不管任务是否完成，立即终止进程。

方法一：主进程运行sing，子进程运行dance。

````python
# 1. 导入进程包。
import multiprocessing
import time
def dance():
    for i in range(3):
        print("Dancing...")
        time.sleep(0.2)
def sing():
    for i in range(3):
        print("Singing...")
        time.sleep(0.2)
# 2. 因为默认有一个进程，自己手动创建的进程为子进程。
dance_process = multiprocessing.Process(target=dance)
# 3. 启动进程，执行对应的任务。
dance_process.start()
# 主进程执行唱歌任务
sing()
````

方法二：主进程创建两个子进程分别运行sing和dance。

```python
# 1. 导入进程包。
import multiprocessing
import time
def dance():
    for i in range(3):
        print("Dancing...")
        time.sleep(0.2)
def sing():
    for i in range(3):
        print("Singing...")
        time.sleep(0.2)
# 2. 因为默认有一个进程，自己手动创建的进程为子进程。
dance_process = multiprocessing.Process(target=dance)
sing_process = multiprocessing.Process(target=sing)
# 3. 启动进程，执行对应的任务。
dance_process.start()
sing_process.start()
# 进程执行是无序的，具体哪个进程先执行是由操作系统调度决定的。
```

## 注意点：

- 进程之间执行顺序是无序的。
- 进程之间不共享全局变量
  - 创建子进程其实是对主进程资源进行拷贝，子进程其实就是主进程的一个副本。
    - 对于linux和mac主进程的代码不会全程拷贝，但是window系统来说主进程执行代码也会进行拷贝。
    - 对于windows来说创建子进程的代码如果进行拷贝执行相当于递归无限制进行创建子进程，会报错。
      - 用`if __name__ == '__main__':` 判断是否是主模块来解决
- 主进程会等等所有子进程执行结束后再结束
  - 如果要实现主进程退出，子进程销毁，有两种方法：
    1. `sub_process.daemon = True` 设置子进程为守护主进程。
    2. `sub_process.termintate()` 主进程退出之前，让子进程销毁。


# Thread

线程

线程是进程中执行代码的一个分支，每个执行分支（线程）要想工作执行代码需要cpu进行调度，也就是说线程是cpu调度的基本单位，每个进程至少都有一个线程，而这个线程就是主线程。

- 除了多进程，多线程也是实现多任务的另一种方式。

1. 导入线程模块

   `import threading`

2. Thread 线程类说明

   **Thread([group [, target [, name [, args [, kwargs]]]]])**

   - group: 线程组，目前只能使用None，不用设置。
   - target: 执行的目标任务名(一个函数或一个方法)。
   - name: 进程名字，一般不会设置，会有默认名字Thread-N。
   - args: 以元组方式给执行任务传参。
   - kwargs: 以字典方式给执行任务传参。

3. 启动进程 start()。

多线程多任务：(三条线程，主线程，两条子线程dance 和 sing)

```python
# 1.导入线程模块
import threading
import time

def sing():
    # 获取当前线程
    current_thread = threading.current_thread()
    print("sing: ", current_thread)

    for i in range(3):
        print("Singing...")
        time.sleep(0.2)

def dance():
    # 获取当前线程
    current_thread = threading.current_thread()
    print("dance: ", current_thread)

    for i in range(3):
        print("Dancing...")
        time.sleep(0.2)

if __name__ == "__main__":
    # 获取当前线程
    current_thread = threading.current_thread()
    print("main_thread: ", current_thread)

    # 2.创建子线程
    sing_thread = threading.Thread(target=sing)
    dance_thread = threading.Thread(target=dance)
    # 3.启动子线程
    sing_thread.start()
    dance_thread.start()
```

## 注意点：

- 线程之间执行顺序是无序的。

- 主线程会等等所有子线程程执行结束后再结束。

  - 如果要实现主线程退出，子线程销毁：
    - `sub_thread.setDaemon(True)` 或 `sub_thread = threading.Thread(target=task, daemon=True)` 设置子线程为守护主线程。

- 单进程多线程中，可以共享全局变量。

  - 因为多线程在同一个进程里面，所以多线程可以共享全局变量。

- 线程之间共享全局变量，数据会出现错误问题。

  - 例如让两个子线程同时分别给全局变量加1，并且执行100万次，会出现错误。

    - **解决方式1：线程等待 (join)**

    - 让第一个线程先执行，然后在让第二个线程再执行，保证数据不会有问题。

    - 保证同一时刻只能有一个线程去操作全局变量。

      ```python
      first_thread.start()
      first_thread.join()
      second_thread.start()
      ```

    - **解决方式2：互斥锁 (lock)**

    - 对共享数据（全局变量）进行锁定，保证同时一时刻只能有一个线程去操作。

    - 互斥锁是多个线程一起去抢，抢到锁的进程先执行（谁先抢到是无法控制的），没有抢到锁的线程需要等待，等互斥锁使用完释放后，其他等待的线程再去抢这个锁。

  - 线程等待和互斥锁都是把多任务改成单任务去执行，保证了数据的准确性，但是执行性能会下降。

# Deadlock

一直等待对方释放锁的情景叫做死锁

```python
import threading

lock = threading.Lock()

def get_value(index):

    lock.acquire()
    my_list = [1, 4, 6]
    
    if index >= len(my_list):
        print("Index out range: ", index)
        # 取值不成功，也需要释放互斥锁，不要影响后面的线程取值，否则会形成死锁。
        lock.release()
        return
    value = my_list[index]
    print("value: ", value)
    
    lock.release()

if __name__ == "__main__":
    for i in range(10):
        sub_thread = threading.Thread(target=get_value, args=(i,))
        sub_thread.start()
```

