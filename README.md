# Getting Started with Jupyter - Creating Reveal.js Slides

## Install Jupyter

Install Anaconda from the [download page](https://www.continuum.io/downloads)

Launch Jupyter Notebook
```
jupyter notebook
```

## Enable the slide toolbar

In the notebook, click on `View -> Cell Toolbar -> Slideshow`. This will add a dropdown to each cell to enable slide type selection (slide, fragment, notes, sub-slide, skip). The dash adds the cell to the previous slide.

## Exporting the slides

Then export the slides with:
```
ipython nbconvert --to slides notebook.ipynb
```

You can serve the slides directly with:
```
ipython nbconvert --to slides notebook.ipynb --post serve
```

## Hide the input from the slides
Create a `input_toggle.tpl` file with this content:
```
{%- extends 'slides_reveal.tpl' -%}

{% block input_group -%}
<div class="input_hidden">
{{ super() }}
</div>
{% endblock input_group %}

{%- block header -%}
{{ super() }}

<script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>

<style type="text/css">
.input_hidden {
  display: none;
}
</style>

<script>
$(document).ready(function(){
  $(".output_wrapper").click(function(){
      $(this).prev('.input_hidden').slideToggle();
  });
})
</script>
{%- endblock header -%}
```

And now serve the slides with:
```
jupyter nbconvert --to slides notebook.ipynb --template input_toggle --post serve
```
