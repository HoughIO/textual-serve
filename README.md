# textual-serve

Every [Textual](https://github.com/textualize/textual) application is now a web application.

With 3 lines of code, any Textual app can run in the browser.




<table>
  <tr>
    <td>
      <p>This is <a href="https://github.com/darrenburns/posting">Posting</a> running in the terminal.</p>
    </td>
    <td>      
      <img src="https://github.com/Textualize/textual-serve/assets/554369/14120e6e-bd8c-4620-a9fc-7cf41e3e994b" width="100%"/>
    </td>
  </tr>
  <tr>
    <td>
      <p>This is <a href="https://github.com/darrenburns/posting">Posting</a> running in the <em>browser</em>.</p>
    </td>
    <td>    
      <img src="https://github.com/Textualize/textual-serve/assets/554369/cfa66f9b-02a0-4335-a127-e5a75c6f859d" width="100%"/>
    </td>    
  </tr>  
</table>

---

## Getting Started

First, [install (or upgrade) Textual](https://textual.textualize.io/getting_started/#installation).

Then install `textual-serve` from PyPI:


```
pip install textual-serve
```

## Creating a server

First import the Server class:

```python
from textual_serve.server import Server
```

Then create a `Server` instance and pass the command that launches your Textual app:

```python
server = Server("python -m textual")
```

The command can be anything you would enter in the shell, as long as it results in a Textual app running.

Finally, call the `serve` method:

```python
server.serve()
```

You will now be able to click on the link in the terminal to run your app in a browser.

### Summary

Run this code, visit http://localhost:8000

```python
from textual_serve.server import Server

server = Server("python -m textual")
server.serve()
```

## Configuration

The `Server` class has the following parameters:

| parameter      | description                                                                        |
| -------------- | ---------------------------------------------------------------------------------- |
| command        | A shell command to launch a Textual app.                                           |
| host           | The host of the web application (defaults to "localhost").                         |
| port           | The port for the web application (defaults to 8000).                               |
| title          | The title show in the web app on load, leave as `None` to use the command.         |
| public_url     | The public URL, if the server is behind a proxy. `None` for the local URL.         |
| statics_path   | Path to statics folder, relative to server.py. Default uses directory in module.   |
| templates_path | Path to templates folder, relative to server.py. Default uses directory in module. |

The `Server.serve` method accepts a `debug` parameter.
When set to `True`, this will enable [textual devtools](https://textual.textualize.io/guide/devtools/).

## How does it work?

When you visit the app URL, the server launches an instance of your app in a subprocess, and communicates with it via a websocket.

This means that you can serve multiple Textual apps across all the CPUs on your system.


Note that Textual-serve uses a custom protocol to communicate with Textual apps.
It *does not* simply expose a shell in your browser.
There is no way for a malicious user to do anything the app-author didn't intend.

## See also

See also [textual-web](https://github.com/Textualize/textual-web) which serves Textual apps on a public URL.

You can consider this project to essentially be a self-hosted equivalent of Textual-web.
