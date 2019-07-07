If you want to render `{% raw %}` and `{% endraw %}` literally,
you can't just nest them in another `raw/endraw` pair.
Instead of letting you nest the tags,
Liquid acts as if the first `endraw` is paired with the first `raw`.
So you're just left with a hanging `endraw` tag and a Liquid syntax error.

The way around this doesn't look so clean in source code, but renders fine
when you build Jekyll.

## This input...
````
{% assign endRaw = "{\% endraw %\}" | replace: "\"  %}
{% assign testvar = "... and now we're out of raw territory" %}

Here's how we work with Liquid:

{% comment %}
*   If you're looking at this in the source, it's not going to make any sense.
*   Serve up Jekyll to see what this looks like rendered.
*         {% endcomment %}

```
{%- raw -%}
{% raw %}
  Code sample
  {{ testvar }}
  {% assign rawfilter = "this should render literally" %}
  {% include nothing.html %}
{% endraw -%}
{{ endRaw }}
{{ testvar }}
```
````
## ...produces this output

Here’s how we work with Liquid:

```
{% raw %}
  Code sample
  {{ testvar }}
  {% assign rawfilter = "this should render literally" %}
  {% include nothing.html %}
{% endraw %}
... and now we're out of raw territory
```
