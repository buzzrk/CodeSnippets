## How to show data as tables in jupyter notebook

```
from IPython.display import HTML, display
def display_table(data):
    html = "<table>"
    for row in data:
        html += "<tr>"
        for field in row:
            html += "<td><h4>%s</h4><td>"%(field)
        html += "</tr>"
    html += "</table>"
    display(HTML(html))```
```

```
t = []
t.append(["Table heading"])
t.append(["Column1","Column2"])
t.append(["Data11","Data21"])
t.append(["Data12","Data22"])
```

