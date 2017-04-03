This Demo Data Package implements an example from [here](http://vega.github.io/vega-editor/?mode=vega&spec=barley/).

In the views spec, we use "Vega Graph Spec" - must be specified in `specType` attribute as `vega` (as in line 39 of code snippet below).
Only difference when using Vega spec is `data` attribute that is removed from the spec (see starting from line 40). Everything else is identical:

<script src="https://gist.github.com/anuveyatsu/4b18a92b7ad805a4459702cf2cba02d4.js"></script>

Outside of `spec` attribute there are some other important parameters to note:

* `name` (lines 36) - unique identifier for view within list of views.

* `title` (lines 37) - title for this graph.

* `resources` (lines 38) - data sources for this spec. It can be either resource name or index. In our example we use resource's index. By default it is the first resource so we could skip this property.

* `specType` (lines 39) - used for defining syntax. In this demo datapackage we use `vega` (Vega Graph Spec).
