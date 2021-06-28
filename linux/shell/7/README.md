

#### 统计文本内字符出现的次数

本命令是要统计words.txt 文件内英文字母 a-z 出现的次数，并且以如下方式展示：
```
A - 276526
B - 27652699
C - 27652699
...
```

```s
if [ -z $1 ] # 如果命令参数为空(-z zero)
then
    echo "Please enter the file of dictionary !"
    exit  # 退出程序
fi

if [ ! -e $1 ] # if判断文件是否存在的命令 -e exist
then
    echo "Please make sure that the file of dictionary exists !"
    exit
fi

# Definition of function
# 函数定义
statistics () {
  for char in {a..z}  # 遍历 a 到 z 字符
  do
    # "$char - `grep -io "$char" $1`"  在文件中查找字符如a，-i 忽略大小写， -o 寻找出所有字符，如果不加，
    #一行中若有多个字符匹配也只认为是找到一行
    # wc -l 统计行数 (-l line)
    # tr /a-z/ /A-Z/  tr是转换， 将小写 a-z 转换 为 A-Z 大写；
    # >> tmp.txt 追加到一个临时用于存储的文件，创造此文件，在于后面能配合sort使用
    echo "$char - `grep -io "$char" $1 | wc -l`" | tr /a-z/ /A-Z/ >> tmp.txt
  done
  # -r 倒序排列， -n 用于对数字排序 ， -k 2 指定 第2列排序 ， -t  - 指定列之间以-作为分隔符
  sort -rn -k 2 -t - tmp.txt
  rm tmp.txt #统计完后，tmp.txt就不需要了，删除掉
}

# Use of function
# 函数使用
statistics $1


```

#### 使用
```s
执行上面的命令：
./statistics.sh words.txt
```














 








