This is an example Data Package, that demonstrates how to build the awesome visualizations using the "Vega Graph Spec". We are using Yields of Barley Based on the [Trellis Display][trellis] - one of the examples from [vega editor][editor] - and displaying it here, on DataHub with slightest modifications in vega-spec.

. This is an example DataPackage that demonstrates usage of "Vega Graph Specifications". This DataPackage is based on this [Vega example](http://vega.github.io/vega-editor/?mode=vega&spec=barley/).


## Views

We assume that you are familiar with what [datapackage.json][datapackage.json] is and it's specifications.

To create graphs for your tabular Data Package, the `datapackage.json` should include the `views` attribute that is responsible for visualizations.

If you are familiar with [Vega][vega] specifications, you would probably like to use all it's futures and display you data with desired visualizations in a Vega way. To use it, inside `views` you should set `specType` to "vega" and define some graph specifications in `spec`. See example datapackage.json:

### Vega Graph Specifications

{{ datapackage.json }}

<br>

You can use almost the same specifications inside `spec` attribute, that are used for setting the vega graphs. Only difference is that in `data` property, `url` and `path` attributes are moved out.

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

Instead we use `name` attribute to reference to a dataset. Note, how we created a new object inside `data` property - `{"name": "barley"}` to reference it to resources (this name is identical to resource name)

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
[datapackage.json]: http://specs.frictionlessdata.io/data-package/#specification
