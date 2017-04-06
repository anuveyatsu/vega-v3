Yields of Barley Based on the [Trellis Display](http://www.jstor.org/stable/1390777) by Becker et al. This is an example DataPackage that demonstrates usage of "Vega Graph Specifications". This DataPackage is based on this [Vega example](http://vega.github.io/vega-editor/?mode=vega&spec=barley/).

## Views

To create graphs for your tabular DataPackage, the datapackage.json should include the views attribute that defines data views.

### Vega Graph Specifications

<script src="https://gist.github.com/anuveyatsu/4b18a92b7ad805a4459702cf2cba02d4.js"></script>

To use "Vega Graph Specification" `specType` inside `views` attribute should be set to `vega` - line 39. You can use almost the same specifications inside `spec` attribute, that are used for setting the vega graphs. Only difference is that in `data` property, all `url` and `path` attributes are moved out. Instead of that, `name` attribute is used to reference a dataset - line 45.

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
