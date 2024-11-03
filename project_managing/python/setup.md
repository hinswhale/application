## 打包
```python setup.py bdist        # 生成平台相关的二进制分发包
python setup.py bdist_wheel  # 生成 Wheel 格式的分发包```


### bdist 文件夹：
当你执行 python setup.py bdist 或 python setup.py bdist_wheel 时，工具会临时创建 bdist.<platform> 文件夹（例如 bdist.macosx-13.0-x86_64）来存放生成的中间文件。
一旦二进制分发文件（如 .whl 或 .tar.gz）成功创建，它们会被移动到 dist 文件夹，bdist 文件夹则会被自动删除。

### build 文件夹：
build 文件夹是另一个临时文件夹，存放构建过程中生成的临时文件。build 文件夹不会自动删除，因为它可能在后续的构建过程中重复使用。你可以手动删除它来清理构建文件。

### dist 文件夹：
dist 文件夹是最终生成分发包的位置。在这里你可以找到项目的分发文件，如*.whl 文件（Wheel 格式*和 **.tar.gz 文件（源代码分发包**。
