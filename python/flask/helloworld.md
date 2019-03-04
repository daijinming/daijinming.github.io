code 
~~~
from flask import Flask

app = Flask(__name__)


@app.route('/')
def hello_world():
    return 'Hello World!'


if __name__ == '__main__':
    app.run()
~~~

# 执行方法：
- `flask run`
- `pipenv run python3 hello.py`
- `python3 hello.py`

# 参考
http://www.cnblogs.com/wangshuyang/p/7754188.html
