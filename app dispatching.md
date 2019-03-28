---


---

<h1 id="folder-structure">Folder structure</h1>
<pre><code>DISPATCHER (folder)
   dispatcher.py

   app1 (folder)
       __init__.py

   app2 (folder)
       __init__.py

   app3 (folder)
       __init__.py
</code></pre>
<blockquote>
<p><a href="http://dispatcher.py">dispatcher.py</a></p>
</blockquote>
<pre><code>from flask import Flask
from werkzeug.wsgi import DispatcherMiddleware
from werkzeug.exceptions import NotFound

from app1 import app as app1
from app2 import app as app2
from app3 import app as app3

app = Flask(__name__)

app.wsgi_app = DispatcherMiddleware(NotFound(), {
    "/app1": app1,
    '/app2': app2,
    '/app3': app3
})

if __name__ == "__main__":
    app.run()
</code></pre>
<p>Set this app1 to app3</p>
<blockquote>
<p><strong>init</strong>.py</p>
</blockquote>
<pre><code>from flask import Flask

app = Flask(__name__)

@app.route("/")
def index_one():
    return "Hi im 1 or 2 or 3"

if __name__ == "__main__":
    app.run()

python app.py

localhost:5000/app1 "Hi im one"
localhost:5000/app2 "Hi im two"
localhost:5000/app3 "Hi im three"
</code></pre>
<p>Another configuratiom</p>
<p>You can import another app, like app0 and add a menu to the apps, changing this with NotFound()</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

