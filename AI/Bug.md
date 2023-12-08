## 模块导入失败

```
Traceback (most recent call last):
  File "D:\Python\lib\site-packages\matplotlib\style\core.py", line 127, in use
    rc = rc_params_from_file(style, use_default_template=False)
  File "D:\Python\lib\site-packages\matplotlib\__init__.py", line 854, in rc_params_from_file
    config_from_file = _rc_params_in_file(fname, fail_on_error=fail_on_error)
  File "D:\Python\lib\site-packages\matplotlib\__init__.py", line 780, in _rc_params_in_file
    with _open_file_or_url(fname) as fd:
  File "D:\Python\lib\contextlib.py", line 119, in __enter__
    return next(self.gen)
  File "D:\Python\lib\site-packages\matplotlib\__init__.py", line 757, in _open_file_or_url
    with open(fname, encoding=encoding) as f:
FileNotFoundError: [Errno 2] No such file or directory: 'deeplearning.mplstyle'

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "D:\Project\Python\MachineLearning\Classification using Logistic Regression.py", line 4, in <module>
    from lib.lab_utils_common import sigmoid
  File "D:\Project\Python\MachineLearning\lib\lab_utils_common.py", line 25, in <module>
    plt.style.use('deeplearning.mplstyle')
  File "D:\Python\lib\site-packages\matplotlib\style\core.py", line 130, in use
    raise IOError(
OSError: 'deeplearning.mplstyle' not found in the style library and input is not a valid URL or path; see `style.available` for list of available styles

```



总结：这是完全黑盒的，不涉及任何知识，就是简单的debug，但是规则不明白，就是很烦躁



leetcode

```
cannot find symbol [in __Driver__.java]
```

解决：

问题的方法名错误



## python模块导入失败

解决办法，删除

import语句

然后利用自带的提示导入包

常见的错误：写了和包名一致的命名，导致导入包一直是自己写的







## numpy数据格式

bug：

```
batch_size should be a positive integer value, but got batch_size=2
```

只能接受普通数据格式：

```python
a=a.tolist()
```

