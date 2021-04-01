# Voting Guide
{% assign total_weight = 0 %}
{% for option in site.data.options %}
  {% assign total_weight = total_weight | plus: option.weight %}
{% endfor %}

{% assign ordered_options = site.data.options | sort: "value" | sort: "weight" | reverse %}
{% for option in ordered_options %}
## {{option.name}}
Value rating: {{option.value}}/5
{% if option.type != "Will" %}
Competitiveness rating: {{option.chance}}/5
{% endif %}
{% if option.weight > 0 %}
Recommended vote share: {{option.weight | times: 100.0 | divided_by: total_weight | round}}%
{% endif %}

{{option.review}}
{% endfor %}