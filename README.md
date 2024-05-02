# CV

<img src="https://countrush-prod.azurewebsites.net/l/badge/?repository=Peg-Wu.wppcv2" style="float: left;"/>

- Owner: Pengpeng Wu (武鹏鹏)
- E-mail: peg2_wu@163.com

# 🐬A quick tutorial of readthedocs

> 🤐最快的使用方式：直接以我的这个仓库为模板进行修改！

## 1. Install Packages

```bash
conda create -n readthedocs python==3.12.1
conda activate readthedocs

pip3 install -U Sphinx
pip3 install sphinx-autobuild
pip3 install sphinx_rtd_theme
pip3 install recommonmark
pip3 install sphinx_markdown_tables
```

## 2. Create Project

```bash
mkdir <project_name>
sphinx-quickstart
```

> 项目创建完成，目录结构如下：
>
> <project_name>
>
> ---- build
>
> ---- make.bat
>
> ---- Makefile
>
> ---- source
>
> -------- conf.py
>
> -------- index.rst
>
> -------- _static
>
> -------- _templates
>
> 
>
> - `Makefile`：可以看作是一个包含指令的文件，在使用 make 命令时，可以使用这些指令来构建文档输出。
> - `build`：生成的文件的输出目录。
> - `make.bat`：Windows 用命令行。
> - `_static`：静态文件目录，比如图片等。
> - `templates`：模板目录。
> - `conf.py`：存放 Sphinx 的配置，包括在 sphinx-quickstart 时选中的那些值，可以自行定义其他的值。
> - `index.rst`：文档项目起始文件。

## 3. Generate HTML files in "build/html"

```bash
make html
```

## 4. Autobuild

直接访问 html 文件不是很方便，所以我们借助 `sphinx-autobuild` 工具启动 HTTP 服务：

```bash
sphinx-autobuild source build/html
```

默认启动 8000 端口，在浏览器输入 [http://127.0.0.1:8000](http://127.0.0.1:8000/) 。

## 5. Modify Theme

```python
# 在conf.py中修改，更多主题: https://sphinx-themes.org/#themes
html_theme = 'sphinx_rtd_theme'
```

## 6. Support Markdown

```python
# 在conf.py中修改
extensions = [
    'recommonmark',
    'sphinx_markdown_tables'
]

# 将index.rst文件后缀改为md, index.md的内容即为readthedocs主页显示的内容~
```

## 7. Rearrange Files

> 将文件组织成如下形式：
>
> <project_name>
>
> ---- docs
>
> -------- build
>
> -------- source
>
> -------- Makefile
>
> -------- make.bat
>
> -------- requirements.txt
>
> ---- .gitignore
>
> ---- .readthedocs.yaml
>
> ---- README.md

(1) 请在`.gitignore`文件中添加：

```txt
docs/build
```

(2) 请在`.readthedocs.yaml`中添加（修改对应的python版本即可）：

```yaml
version: "2"

build:
  os: "ubuntu-22.04"
  tools:
    python: "3.12"

python:
  install:
    - requirements: docs/requirements.txt

sphinx:
  configuration: docs/source/conf.py
```

(3) `docs/requirements.txt`文件由如下命令生成：

```bash
conda activate readthedocs
pip freeze > requirements.txt
```

## 8. Upload to github & readthedocs, Done!

- readthedocs: https://readthedocs.org/
