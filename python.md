# Python

## Pandas

### Get Start
```python
import pandas # sometimes as pd
```

### DataFrame.dropna()
```python
df.dropna(
    axis: 'Axis' = 0, # {0 or 'index', 1 or 'columns'}, default 0
    how: 'str' = 'any', # {'any', 'all'}, default 'any'
    thresh=None, # int, optional
    subset: 'IndexLabel' = None, # column label or sequence of labels, optional
    inplace: 'bool' = False, # bool, default False
) 
# Returns DataFrame or None
# DataFrame with NA entries dropped from it or None if inplace=True.
```

### 画图 DataFrame.plot()/Series.plot()
```python
DataFrame.plot(x=None, y=None, kind='line', ax=None, subplots=False, 
                sharex=None, sharey=False, layout=None,figsize=None, 
                use_index=True, title=None, grid=None, legend=True, 
                style=None, logx=False, logy=False, loglog=False, 
                xticks=None, yticks=None, xlim=None, ylim=None, rot=None,
                xerr=None,secondary_y=False, sort_columns=False, **kwds)
                
#参数详解
Parameters:
x : label or position, default None#指数据框列的标签或位置参数

y : label or position, default None

kind : str
‘line’ : line plot (default)#折线图
‘bar’ : vertical bar plot#条形图
‘barh’ : horizontal bar plot#横向条形图
‘hist’ : histogram#柱状图
‘box’ : boxplot#箱线图
‘kde’ : Kernel Density Estimation plot#Kernel 的密度估计图，主要对柱状图添加Kernel 概率密度线
‘density’ : same as ‘kde’
‘area’ : area plot#不了解此图
‘pie’ : pie plot#饼图
‘scatter’ : scatter plot#散点图  需要传入columns方向的索引
‘hexbin’ : hexbin plot#不了解此图

ax : matplotlib axes object, default None#**子图(axes, 也可以理解成坐标轴) 要在其上进行绘制的matplotlib subplot对象。如果没有设置，则使用当前matplotlib subplot**其中，变量和函数通过改变figure和axes中的元素（例如：title,label,点和线等等）一起描述figure和axes，也就是在画布上绘图。

subplots : boolean, default False#判断图片中是否有子图
Make separate subplots for each column

sharex : boolean, default True if ax is None else False#如果有子图，子图共x轴刻度，标签
In case subplots=True, share x axis and set some x axis labels to invisible; defaults to True if ax is None otherwise False if an ax is passed in; Be aware, that passing in both an ax and sharex=True will alter all x axis labels for all axis in a figure!

sharey : boolean, default False#如果有子图，子图共y轴刻度，标签
In case subplots=True, share y axis and set some y axis labels to invisible

layout : tuple (optional)#子图的行列布局
(rows, columns) for the layout of subplots

figsize : a tuple (width, height) in inches#图片尺寸大小

use_index : boolean, default True#默认用索引做x轴
Use index as ticks for x axis

title : string#图片的标题用字符串
Title to use for the plot

grid : boolean, default None (matlab style default)#图片是否有网格
Axis grid lines

legend : False/True/’reverse’#子图的图例，添加一个subplot图例(默认为True)
Place legend on axis subplots

style : list or dict#对每列折线图设置线的类型
matplotlib line style per column

logx : boolean, default False#设置x轴刻度是否取对数
Use log scaling on x axis
logy : boolean, default False
Use log scaling on y axis

loglog : boolean, default False#同时设置x，y轴刻度是否取对数
Use log scaling on both x and y axes

xticks : sequence#设置x轴刻度值，序列形式（比如列表）
Values to use for the xticks

yticks : sequence#设置y轴刻度，序列形式（比如列表）
Values to use for the yticks

xlim : 2-tuple/list#设置坐标轴的范围，列表或元组形式
ylim : 2-tuple/list

rot : int, default None#设置轴标签（轴刻度）的显示旋转度数
Rotation for ticks (xticks for vertical, yticks for horizontal plots)

fontsize : int, default None#设置轴刻度的字体大小
Font size for xticks and yticks

colormap : str or matplotlib colormap object, default None#设置图的区域颜色
Colormap to select colors from. If string, load colormap with that name from matplotlib.

colorbar : boolean, optional  #图片柱子
If True, plot colorbar (only relevant for ‘scatter’ and ‘hexbin’ plots)

position : float   
Specify relative alignments for bar plot layout. From 0 (left/bottom-end) to 1 (right/top-end). Default is 0.5 (center)

layout : tuple (optional)  #布局
(rows, columns) for the layout of the plot

table : boolean, Series or DataFrame, default False  #如果为正，则选择DataFrame类型的数据并且转换匹配matplotlib的布局。
If True, draw a table using the data in the DataFrame and the data will be transposed to meet matplotlib’s default layout. If a Series or DataFrame is passed, use passed data to draw a table.

yerr : DataFrame, Series, array-like, dict and str
See Plotting with Error Bars for detail.

xerr : same types as yerr.

stacked : boolean, default False in line and
bar plots, and True in area plot. If True, create stacked plot.

sort_columns : boolean, default False  # 以字母表顺序绘制各列，默认使用前列顺序

secondary_y : boolean or sequence, default False  ##设置第二个y轴（右y轴）
Whether to plot on the secondary y-axis If a list/tuple, which columns to plot on secondary y-axis

mark_right : boolean, default True
When using a secondary_y axis, automatically mark the column labels with “(right)” in the legend

kwds : keywords
Options to pass to matplotlib plotting method

Returns:axes : matplotlib.AxesSubplot or np.array of them
```

### 滚动窗口 DataFrame.rolling()
```python
df = tushare.get_hist_data('601318')

#循环方法实现滑动平均
for i in range(4,len(df)):
    df.loc[df.index[i],'ma5'] = df['close'][i-4:i+1].mean()
for i in range(29,len(df)): 
    df.loc[df.index[i],'ma30'] = df['close'][i-29:i+1].mean()
 
#不用循环实现滑动平均    
#5行移动平均 moving average
df['ma5'] = df['close'].rolling(5).mean()
#30行移动平均 moving average
df['ma30'] = df['close'].rolling(30).mean()

```

### 



## Tushare

### Get Start
```python
import tushare # sometimes as te/tu/ts
```
#### get a stock

##### old version tushare.get_hist_data()
```python
df = tushare.get_hist_data('601318')
```
##### new version pro.daily(ts_code,start_date,end_date)
```python
pro = ts.pro_api()

#单只股票
df = pro.daily(ts_code='000001.SZ', start_date='20180701', end_date='20180718')

#多个股票
df = pro.daily(ts_code='000001.SZ,600000.SH', start_date='20180701', end_date='20180718')
#或者
df = pro.query('daily', ts_code='000001.SZ', start_date='20180701', end_date='20180718')

#也可以通过日期取历史某一天的全部历史
df = pro.daily(trade_date='20180810')
```

## Type hint
To clarify the type of input and output, in static way.
This will be showed by the IDE when called, for easy usage
```python
def f(a: int, b: int) -> int:
    return a+b
```
### Static analysis tool
```shell
# this will help analysis the code by the static type int
pip install mypy

# check by mypy
mypy example.py
```

### self defined type in type hint
```python
class A:
    name = 'A'

def get_name(o: A) -> str:
    return o.name

get_name(A) #会报错，type不是A()
get_name(A())
```

When the return type is the type itself,
use type name as a string, to interpret later
```python
class Node:
    def __init__(self,prev: "Node"):
        self.prev = prev
        self.next = None
```

### Recursive type usage, e.g. list
```python
def my_sum(lst: list) -> int:
    total = 0
    for i in lst:
        total += i
    return total

my_sum([0,1,2]) #例1
my_sum(1) #例2 会报错，type不是list
my_sum(['0',1,2]) #例3 不会报错，因为第一层还是list

# python3.9+ 这样表示list中都是int，上述例子3就会报错
def my_sum(lst: list[int]) -> int:
    pass

# python3.9-
from typing import List
def my_sum(lst: List[int]) -> int:
    pass

my_sum((0,1,2)) #例4 会报错，因为tuple不是list

from typing import Sequence
def my_sum(lst: Sequence[int]) -> int:
    pass

my_sum((0,1,2)) #例4 不会报错
my_sum(range(3)) #例5
my_sum(b"012") #例6
```

### Dictionary type
```python
def my_sum(d: dict[str,int]) -> int:
    total = 0
    for i in d.values:
        total += i
    return total

my_sum({"a":1,"b":2,"c":3}) 
my_sum({"a":1,"b":2,"c":"3"}) #会报错
```

### Multiple possible types/ None type args
```python
from typing import Union
def f(x: Union[int,None]) -> int:
    if x is None:
        return 0
    return x

f(None)
f(0)

# after python3.10
def f(x: int | None) -> int:
    pass

# 如果只有一个类型或者None
from typing import Optional
def f(x: Optional[int]) -> int:
    pass 

```

## Comment

Refer to the link for details
https://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/python_style_rules

### Comments in functions 
```python
def fetch_smalltable_rows(table_handle: smalltable.Table,
                        keys: Sequence[Union[bytes, str]],
                        require_all_keys: bool = False,
) -> Mapping[bytes, Tuple[str]]:
    """Fetches rows from a Smalltable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by table_handle.  String keys will be UTF-8 encoded.

    Args:
    table_handle:
        An open smalltable.Table instance.
    keys:
        A sequence of strings representing the key of each table row to
        fetch.  String keys will be UTF-8 encoded.
    require_all_keys:
        Optional; If require_all_keys is True only rows with values set
        for all keys will be returned.

    Returns:
    A dict mapping keys to the corresponding table row data
    fetched. Each row is represented as a tuple of strings. For
    example:

    {b'Serak': ('Rigel VII', 'Preparer'),
    b'Zim': ('Irk', 'Invader'),
    b'Lrrr': ('Omicron Persei 8', 'Emperor')}

    Returned keys are always bytes.  If a key from the keys argument is
    missing from the dictionary, then that row was not found in the
    table (and require_all_keys must have been False).

    Raises:
    IOError: An error occurred accessing the smalltable.
    """
```

### Comments in Class
```python
class SampleClass(object):
    """Summary of class here.

    Longer class information....
    Longer class information....

    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam=False):
        """Inits SampleClass with blah."""
        self.likes_spam = likes_spam
        self.eggs = 0

    def public_method(self):
        """Performs operation blah."""
```