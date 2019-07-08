### jupyter
---
http://jupyter.org/

https://github.com/jupyter/notebook

https://github.com/markusschanta/awesome-jupyter

```sh
pip install notebook
jupyter notebook
```

```py
var cell = Jupyter.notebook.get_selected_cell();
var config = cell.config;
var patch = {
  CodeCell:{
    cm_config:{indentUnit:2}
  }
}
config.update(patch)

var cell = Jupyter.notebook.get_selected_cell();
var config = cell.config;
var patch = {
  CodeCell:{
    cm_config:{indentUnit: null}
  }
}
config.update(patch)

def _jupyter_server_extension_paths():
  return [{
    "module": "my_module"
  }]

def load_jupyter_server_extension(nbapp):
  nbapp.log.info("my module enabled!")
```

```yml
- setup.py
- MANIFEST.in
- my_module/
  - __init__.py
```

