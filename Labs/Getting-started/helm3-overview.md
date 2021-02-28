# Helm3

Helm is commonly known as a Kubernetes package manager. It's a way to combine multiple Kubernetes resouces into a single deployable artefact that contains all the necessary Kubernetes resources to deploy an application OpenShift. OpenShift ships with Helm3 compatibility out of the box, all that is required by the user to use it is to install the Helm3 command line interface.

Helm is a tool for managing Kubernetes packages called charts. Helm can do the following:

- Create new charts from scratch
- Package charts into chart archive (tgz) files
- Interact with chart repositories where charts are stored
- Install and uninstall charts into an existing Kubernetes cluster
- Manage the release cycle of charts that have been installed with Helm

# Templating Language
All Helm resources, when packaged, run through a Go templating engine which dynamically generates values based on the template code evaluation. Using this templating language each deployment can be customised with a unique set of values for the release. This guide will not extensively cover all of the template functions available. More information can be found in the reference articles section. The templating code is embedded into the Kubernetes resource file, replacing the values of fields you wish to allow the user to specify.

If you're new to Helm. this section may not make much sense until you have developed a Helm chart (covered later).  

Some basic but effective examples are below

**White Space Trimming**
White space in YAML files can be a problem, and not always easy to debug. When developing Helm charts you should take care when using template functions that you do not generate unwanted white space (and subsequently, bad parameter mapping). You can trim white space at the start of a template function by using `-`.

Space to the left of the function **not** trimmed

```
data:
  {{ if .Values.key1.value }}
  key1: {{ .Values.key1.value }}
  {{ end }}
```
Which would later cause an error similar to `Error: YAML parse error on mychart/templates/configmap.yaml: error converting YAML to JSON: yaml: line 9: did not find expected key` as it produces
```
data:
    key1: value1
```
As you can see, the `key1` parameter is incorrectly indented. With the function **trimmed**
```
data:
  {{- if .Values.key1.value }}
  key1: {{ .Values.key1.value }}
  {{- end }}
```
This produces the desired result
```
data:
  key1: value1
```

**If/Else**
In this example, there is an 'if' block that will print `mug: true` if the `.Values.favorite.drink` value is 'coffee', else it will print `glass: true`
```
beverage:
  {{- if eq .Values.favorite.drink "coffee"}}
  mug: true
  {{- else }}
  glass: true
  {{- end}}
```
If the value passed to the template engine is 'coffee' then the below will be generated when the chart is packaged
```
beverage:
  mug: true
```

**with**
Using `with` sets the scope of the `.Values` so that references to a particular variable can be shorter. For example, with a value scope of `.Values.favorite.drink` we can do
```
favorite:
  {{- with .Values.favorite.drink }}
  champagne: {{ .champagne | quote }}
  coffee: {{ .coffee | quote }}
  tea: {{ .tea | quote }}
  {{- end }}
```
This is instead of using
```
favorite:
  champagne: {{ .Values.favorite.drink.champagne }}
  coffee: {{ .Values.favorite.drink.coffee }}
  tea: {{ .Values.favorite.drink.tea }}
```

**Range**
The range function allows you to loop through a list (and apply a prefix/suffix). It will iterate through an array and print the output. For example, to iterate through an array of items `["item1","item2","item3"]`
```
items: |-
  {{- range .Values.items }}
  - {{ . | quote }}
  {{- end }}
```
This would produce
```
items:
  - item1
  - item2
  - item3
```

**toYaml/toJson**
These functions are useful if you want end users to supply valid YAML or JSON data as a parameter. In this case, the in-built parser will attempt to output correct YAML or JSON, so it's important that the data is supplied correctly. Any valid YAML or JSON formatted data is accepted. For example, passing a simple JSON list in the format `{"key1:"value1","key2":"value2","key3":"value3"}` with the template
```
keys:
  {{- toYaml .Values.keys | indent 2 }}
```
produces
```
keys:
  key1: value1
  key2: value2
  key3: value3
```
Note the `indent` function is used here to indent the output by 2 spaces.

More complex structured data can also be used, so ensure that the data you supply is correct JSON.

One limitation to `toYaml` is if the data supplied is a literal string (enclosed in single quotes) then it is still valid YAML, so will be printed out as a literal string and not expanded to YAML.

**Commenting**

Commenting within a template can be done by using `{{/*` to open and `*/}}` to close.
```
{{/*
This is a comment that describes the next section
*/}}
```