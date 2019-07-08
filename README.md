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
  
def _jupyter_server_extension_paths():
  return [{
    "module": "my_fancy_module"
  }]
  
def _jupyter_nbextension_paths():
  return [dict(
    section="notebook",
    src="static",
    dest="my_fancy_module",
    require="my_fancy_module/index")]
    
def load_jupyter_server_extension(nbapp):
  nbapp.log.info("my module enbaled!")

import setuptools

setuptools.setup(
  name="MyFancyModule",
  include_package_data=True,
  data_files=[
    ("share/jupyter/nbextensions/my_fancy_module", [
      "my_fancy_module/static/index.js",
    ]),
    ("etc/jupyter/nbconfig/notebook.d", [
      "jupyter-config/nbconfig/notebook.d/my_fancy_module.json"
    ]),
    ("etc/jupyter/jupyter_notebook_config.d", [
      "jupyter-config/jupyter_notebook_config.d/my_fancy_module.json"
    ])
  ],
  zip_safe=False
)

import tarfile
import io
import os
import nbformat

def _jupyter_bundlerextension_paths():
  """ """
  return [{
    "name": "tarball_bundler",
    "module_name": "my_tarball_bundler",
    "label": "Notebook Tarball (tar.gz)",
    "group": "download"
  }]
  
def bundle(handler, model):
  """
  """
  notebook_filename = model['name']
  notebook_content = nbformat.writes(model['content']).encode('utf-8')
  notebook_name = os.path.splitext(notebook_filename)[0]
  tar_filename = ''.format(notebook_name)
  
  info = tarfile.TarInfo(notebook_filename)
  info.size = len(notebook_content)
  
  with io.ByteIO() as tar_buffer:
    with tarfile.open(tar_filename, "w:gz", fileobj=tar_buffer) as tar:
      tar.addfile(info, io.BytesIO(notebook_content))
      
    handler.set_header('Content-Disposition',
      'attachment; filename="{}"'.format(tar_filename))
    handler.set_header('Content-Type', 'application/gzip')
    handler.finish(tar_buffer.getvalue())
```

```yml
- setup.py
- MANIFEST.in
- my_module/
  - __init__.py
```

