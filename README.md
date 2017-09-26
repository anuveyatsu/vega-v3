This is an example dataset that demonstrates how to build visualizations using the "Vega Graph Spec". We are using Yields of Barley Based on the [Trellis Display][trellis] - one of the examples from [vega editor][editor] - and displaying it here, on DataHub with small modifications in vega-spec.

## Views

We assume that you are familiar with what [datapackage.json][datapackage.json] is and its specifications.

To create graphs for your tabular data, the `datapackage.json` should include the `views` attribute that is used for visualizations.

If you are familiar with [Vega][vega] specifications, you probably would like to use all its features. To use it, inside `views` you should set `specType` to `"vega"` and define some graph specifications in `spec` property. See below for more details.

### Vega Graph Specifications

This is the `views` property that is used for this page:

```
{
  ...,
  "views": [
    {
      "title": "DEMO Vega spec view",
      "resources": ["barley"],
      "specType": "vega",
      "spec": {
        "width": 200,
        "height": 720,
        "data": [
          {
            "name": "barley"
          }
        ],
        "scales": [
          {
            "name": "g",
            "type": "ordinal",
            "range": "height",
            "padding": 0.15,
            "domain": {
              "data": "barley", "field": "site",
              "sort": {"field": "yield", "op": "median"}
            },
            "reverse": true
          },
          {
            "name": "x",
            "type": "linear",
            "nice": true,
            "range": "width",
            "domain": {"data": "barley", "field": "yield"}
          },
          {
            "name": "c",
            "type": "ordinal",
            "range": "category10",
            "domain": {"data": "barley", "field": "year"}
          }
        ],
        "axes": [
          {"type": "x", "scale": "x"}
        ],
        "legends": [
          {"fill": "c", "title": "year"}
        ],
        "marks": [
          {
            "name": "sites",
            "type": "group",
            "from": {
              "data": "barley",
              "transform": [{"type": "facet", "groupby": ["site"]}]
            },
            "scales": [
              {
                "name": "y",
                "type": "ordinal",
                "range": "height",
                "points": true,
                "padding": 1.2,
                "domain": {
                  "data": "barley", "field": "variety",
                  "sort": {"field": "yield", "op": "median"}
                },
                "reverse": true
              }
            ],
            "axes": [
              {
                "type": "y",
                "scale": "y",
                "tickSize": 0,
                "properties": {"axis": {"stroke": {"value": "transparent"}}}
              }
            ],
            "properties": {
              "enter": {
                "x": {"value": 0.5},
                "y": {"scale": "g", "field": "key"},
                "height": {"scale": "g", "band": true},
                "width": {"field": {"group": "width"}},
                "stroke": {"value": "#ccc"}
              }
            },
            "marks": [
              {
                "type": "symbol",
                "properties": {
                  "enter": {
                    "x": {"scale": "x", "field": "yield"},
                    "y": {"scale": "y", "field": "variety"},
                    "size": {"value": 50},
                    "stroke": {"scale": "c", "field": "year"},
                    "strokeWidth": {"value": 2},
                    "fill": {"value": "transparent"}
                  }
                }
              }
            ]
          },
          {
            "type": "text",
            "from": {"mark": "sites"},
            "properties": {
              "enter": {
                "x": {"field": {"group": "width"}, "mult": 0.5},
                "y": {"field": "y", "offset": -2},
                "fontWeight": {"value": "bold"},
                "text": {"field": "datum.site"},
                "align": {"value": "center"},
                "baseline": {"value": "bottom"},
                "fill": {"value": "#000"}
              }
            }
          }
        ]
      }
    }
  ]
}
```

<br>

You can use almost the same specifications inside `spec` attribute, that are used for setting the Vega graphs. Only difference is that in `data` property, `url` and `path` attributes are moved out. Instead we use `name` attribute to reference to a resource. Note, how we created a new object inside `data` property - `{"name": "flights-airport"}` to reference it to a resource (this names are identical to names of resources):

```
  ...
  "spec": {
    ...
    "data": [
      {
        "name": "barley"
      }
      ...
    ]
    ...
  }
```

Outside of `spec` attribute there are some other important parameters to note:

<table class="table table-bordered table-striped resource-summary">
  <thead>
   <tr>
     <th>Attribute</th>
     <th>Type</th>
     <th>Description</th>
   </tr>
  </thead>
  <tbody>
    <tr>
      <th>name</th>
      <td>String</td>
      <td>Unique identifier for view within list of views.</td>
    </tr>
    <tr>
      <th>title</th>
      <td>String</td>
      <td>Title for the graph.</td>
    </tr>
    <tr>
      <th>resources</th>
      <td>Array</td>
      <td>Data sources for this spec. It can be either resource name or index. By default it is the first resource.</td>
    </tr>
    <tr>
      <th>specType</th>
      <td>String</td>
      <td>Available options: simple, vega, plotly <strong>(Required)</strong>.</td>
    </tr>
  </tbody>
</table>

[vega]: https://vega.github.io/vega/
[trellis]: http://www.jstor.org/stable/1390777
[editor]: https://vega.github.io/vega-editor/?mode=vega&spec=barley
[datapackage.json]: http://specs.frictionlessdata.io/data-package/
