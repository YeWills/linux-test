

#### 生成缩略图并html展示
注意，要安装缩略图插件：
```s
 yum install ImageMagick
```

```s
#!/bin/bash

# 如果命令参数为空(-z zero)，就用默认的gallery.html
if [ -z $1 ]
then
    output='gallery.html'
else
    output=$1
fi

# 使用空字符串替换文件内容  >输出重定向
echo '' > $output

if [ ! -e thumbnails ]  # 如果不存在thumbnails目录
then
    mkdir thumbnails
fi

# Beginning of HTML（HTML 文件的开头）
echo '<!DOCTYPE html>
<html>
  <head>
    <title>My Gallery</title>
  </head>
  <body>
    <p>' >> $output  #`>>` 重定向文件末尾

#  `2>` 将错误信息输出重定向到文件中， /dev/null是黑洞目录，完全丢弃
for image in `ls *.jpg *.png *.jpeg *.gif 2>/dev/null` 
do
    convert $image -thumbnail '200x200>' thumbnails/$image  #压缩的图片放置thumbnails/目录下
    echo '      <a href="'$image'"><img src="thumbnails/'$image'" alt=""/></a>' >> $output
done

# End of HTML（HTML 文件的结尾）
echo '    </p>
  </body>
</html>' >> $output

```

#### 使用
```s
执行上面的命令：
./gallery.sh test.html
```














 








