django-jsmetatemplates
======================

Template tag library for building building javascript templates using django templates


Allows for javascript templates (like moustache.js ones) to be built using the inheritence
and include functionality of django-templates before being rendered to the client.

Gets around the problem of overlapping delimiters by using a different delimiter for javascript templates
that is then turned into the correct one during django template rendering.

An example:

js\_template\_base.html:
```html
<div>
	<h1>{! title !}</h1>
	{% block content %}
	{% endblock %}
</div>
```

js\_template\_derivative.html:
```html
{% extends 'js\_template\_base.html' %}

{% block content %}
<ul>
	<li>{! thing\_one !}</li>
	<li>{! thing\_two !}</li>
</ul>
{% endblock %}
```

page\_template.html:
```html
{% load jsmetatemplate %}

{% include\_ichtemplate "js\_template\_derivative.html" %}
```

page\_template.html will then render to:
```html
<script type="text/html" id="js\_template\_derivative.html">
<div>
	<h1>{{ title }}</h1>
	<ul>
		<li>{{ thing\_one }}</li>
		<li>{{ thing\_two }}</li>
	</ul>
</div>
</script>
```