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

```

```
```

