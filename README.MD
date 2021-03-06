### 功能描述：

    将深圳市电子发票贴到公司报销单模板中，并导出为pdf文件。

### 注意事项：

只能运行在windows上，且已经安装了ms office。

### 依赖：

- python 3.7
- python-pptx 负责操作pptx
- PyMuPDF 负责操作pdf
- comtypes 负责调用系统已安装的ppt程序，导出pdf
- PyPDF2用于合并多个pdf文件

### 安装：

1. 安装python3.7

2. 安装对应的第三方库

```
pip install -r requirements.txt
```

### 使用步骤：

1、将电子发票pdf文件放到"inputs"文件夹；

2、运行如下脚本，在"outputs"文件夹生成的pdf票据文件；

```shell
python .\invoice_converter.py
```

### 实现思路：

完全按照手动贴票的流程进行：

电子发票pdf------>PNG图片------>插入pptx模板（调整位置、大小）------>导出pdf文件

### 已知问题：

1、使用Cmder 运行脚本报错，无法调用ms office。请改用系统自带PowerShell执行。

### 更新说明：

v2.0

新增自动填写文字部分内容。

前提：电子发票必须以金额数字命名。（如：27.60.pdf，如果金额相同，可以多加几个0保持文件唯一性，如27.600.pdf）

- 场景1：发票全部都是电子发票

  将电子发票按照金额命名后，放入inputs文件夹中，执行下面命令：

  ```sh
  python .\invoice_converter.py [经办人姓名]
  ```

  

- 场景2：有部分是纸质发票，这里只输出电子发票部分。执行脚本需要额外传入`凭证总张数`和`凭证总金额`，执行如下命令：

  ```sh
  python .\invoice_converter.py [经办人姓名] [凭证总张数] [凭证总金额]
  ```

  **注意：这种方式，后续的纸质发票黏贴单，每页只能有黏贴一张发票才能保证`本页张数`正确。**