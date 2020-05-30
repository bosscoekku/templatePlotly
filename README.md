# How to deploy dash 
demo project : https://template-plotly.herokuapp.com/
###### 1. Create project
```shell
mkdir template-plotly
cd template-plotly
```
###### 2. Create virtualenv
```shell
py -m venv env
env\Scripts\activate      # activate env
```
###### 3. install Package
```shell
pip install dash
pip install gunicorn   # for deploy server
```
###### 4. Create file app.py
```shell
touch app.py
```
```python
# code in file app.py
import os

import dash
import dash_core_components as dcc
import dash_html_components as html

external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

app = dash.Dash(__name__, external_stylesheets=external_stylesheets)

server = app.server

app.layout = html.Div([
    html.H2('Hello World'),
    dcc.Dropdown(
        id='dropdown',
        options=[{'label': i, 'value': i} for i in ['LA', 'NYC', 'MTL']],
        value='LA'
    ),
    html.Div(id='display-value')
])

@app.callback(dash.dependencies.Output('display-value', 'children'),
              [dash.dependencies.Input('dropdown', 'value')])
def display_value(value):
    return 'You have selected "{}"'.format(value)

if __name__ == '__main__':
    app.run_server(debug=True)
```


###### 4. Create file .gitignore
```shell
touch .gitignore
```
```shell
env
*.pyc
.DS_Store
.env
```

###### 5. Create file Procfile
```shell
touch Procfile
```
```shell
web: gunicorn app:server
```
###### 6. Create file requirements.txt
```shell
pip freeze > requirements.txt
```
###### 7. git setup
```shell
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/bosscoekku/templatePlotly.git
git push -u origin master
                
```