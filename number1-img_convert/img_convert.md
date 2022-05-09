# 1. 先决条件

## 1.1 图像的构造
一张图片是由若干给像素块构成，我们需要把图片转为字符串图片，就是使用字符去填充每一个像素块。

## 1.2 灰度值
图像由工业界RGB颜色标准，通过3种颜色的互相叠加覆盖几乎所有的色域，我们需要把RGB色彩转为黑白色彩，根据黑和白的程度不同划分一个0~255的区间，黑色是0，白色255

## 1.3 Pillow库（图像处理库）
```shell
pip install -i http://pypi.douban.com/simple --trusted-host pypi.douban.com pillow
1
```

# 2. 代码实现
* 2.1 先将RGB转换为256灰度值
```python
'''
简单的RGB->灰度值公式
gray = int(0.2126 * r + 0.7152 * g + 0.0722 * b)  # 计算灰度
'''
```

* 2.2 然后把灰度值映射到70个字符上
```python
'''
ascii_char = list(r"wmzвгдеёжзийклмнопрсoahkbdpqjftZO0QLCJ YX/\|()1{}[]?-_+~<>i!lI;:,\"^`'. ")
length代表字串的长度，让70个字符等分256个灰度域
unit = (256.0 + 0) / length
'''
```

* 2.3 处理图片
```python
'''
Image.open(image_file) 打开文件
im.resize((WIDTH, HEIGHT), Image.NEAREST) 重新设置图片大小
Image.ANTIALIAS: 高质量
    Image.NEAREST: 低质量
    Image.BILINEAR: 双线性
    Image.BICUBIC: 三次样条插值
'''
```

2.4 文本输出
```python
'''
for i in range(HEIGHT):
    for j in range(WIDTH):
        txt += get_char(*im.getpixel((j, i)))
    txt += '\n'
'''
```

> 参考文档: https://blog.csdn.net/xw1680/article/details/105349156