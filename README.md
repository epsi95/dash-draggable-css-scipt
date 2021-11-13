# dash-draggable-css-scipt
```python
import dash
import dash_core_components as dcc
import dash_html_components as html
import dash_bootstrap_components as dbc
from dash.dependencies import Input, Output, State, ClientsideFunction


app = dash.Dash(
    __name__,
    external_scripts=["https://cdnjs.cloudflare.com/ajax/libs/dragula/3.7.2/dragula.min.js", "https://raw.githubusercontent.com/epsi95/dash-draggable-css-scipt/main/script.js"],
    external_stylesheets=[dbc.themes.BOOTSTRAP, "https://raw.githubusercontent.com/epsi95/dash-draggable-css-scipt/main/dragula.css"]
)

app.layout = html.Div(id="main", children=[
    html.Div(id="drag_container", className="container", children=[
        dbc.Card([
            dbc.CardHeader("Card 1"),
            dbc.CardBody(
                "Some content"
            ),
        ]),
        dbc.Card([
            dbc.CardHeader("Card 2"),
            dbc.CardBody(
                "Some other content"
            ),
        ]),
        dbc.Card([
            dbc.CardHeader("Card 3"),
            dbc.CardBody(
                "Some more content"
            ),
        ]),
    ]),
])

app.clientside_callback(
    ClientsideFunction(namespace="clientside", function_name="make_draggable"),
    Output("drag_container", "data-drag"),
    [Input("drag_container", "id")],
)

if __name__ == "__main__":
    app.run_server(debug=True)
```
