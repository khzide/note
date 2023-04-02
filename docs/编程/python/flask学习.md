# flask学习笔记



### 快速开始

#### 设置flask运行环境变量: 

在命令行中

```c
>set FLASK_APP = hello
>flask run --host=0.0.0.0 --port=80    
```

在powershell中

```c
>$env:FLASK_APP="hello"
>flask run    
```

当flask运行应用名为app.py或wsgi.py时，可以不设置FLASK_APP环境变量。



#### 调试模式，可以显示错误堆栈在流览器中。

```c
>$env:FLASK_DEBUG=1
> flask run
```

通过设置development  自动启动调试模式

```c
(.venv) PS E:\cod\python\temp\4> flask run
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000 (Press CTRL+C to quit)
(.venv) PS E:\cod\python\temp\4> $env:FLASK_ENV='development'
(.venv) PS E:\cod\python\temp\4> flask run
 * Environment: development
 * Debug mode: on
 * Running on http://127.0.0.1:5000 (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 969-211-910
```



#### html转义

escape(str)  对str进行转义,常用于用户录入的值，可防止注入攻击。

#### URL变量类型

| `string` | （默认）接受任何不带斜线的文本 |
| -------- | ------------------------------ |
| `int`    | 接受正整数                     |
| `float`  | 接受正浮点值                   |
| `path`   | 像`string`但接受斜线           |
| `uuid`   | 接受 UUID 字符串               |

#### url尾部/ 和重定向

示例:

@app.route('/project/')

@app.route('/abort')

以/结尾的url地址类似于文件夹，用户录入/project时，会自动重定向到/project/.

不以/结尾的url类似于文件，用户录入/abort/时，会报404未找到错误。

#### url_for 通过函数名进行网址构建

* 生成的路径总是绝对路径。
* 如果函数在url根目录之前，也可以正确构建。
* 可以自动（透明）地处理特殊字符的转义。

```python
from flask import url_for

@app.route('/')
def index():
    return 'index'

@app.route('/login')
def login():
    return 'login'

@app.route('/user/<username>')
def profile(username):
    return f'{username}\'s profile'

with app.test_request_context():
    print(url_for('index'))
    print(url_for('login'))
    print(url_for('login', next='/'))
    print(url_for('profile', username='John Doe'))
```

结果：

```python
/
/login
/login?next=/
/user/John%20Doe
```



#### 渲染模板JianJia2

 模板中可以访问config, request, session, g对象，url_for, get_flashed_messages 函数。

```python
from markupsafe import Markup
Markup('<strong>Hello %s!</strong>') % '<blink>hacker</blink>'
Markup('<strong>Hello &lt;blink&gt;hacker&lt;/blink&gt;!</strong>')
Markup.escape('<blink>hacker</blink>')
Markup('&lt;blink&gt;hacker&lt;/blink&gt;')
Markup('<em>Marked up</em> &raquo; HTML').striptags()
'Marked up » HTML'
```

#### 重定向及错误

```python
from flask import abort, redirect, url_for

@app.route('/')
def index():
    return redirect(url_for('login'))

@app.route('/login')
def login():
    abort(401)
    this_is_never_executed()
```

#### 响应response

make_response 创建响应



# 深入理解flask

## Blueprint

```python
# 在每次用户请求之前或之后触发，
@app.befor_request
@app.teardown_request

# 错误页面
@app.errorhandler(404)
def page_not_found(error):
    return render_template('pagenotfound.html'),404
```

