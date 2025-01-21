layout: page
title: Reverse

permalink: Reverse/
---
# Reverse


				HTML
				
					
				
				
						
				
			
  {% for page in site.pages %}
    {% if page.path contains "Reverse/" and page.path contains ".md" %}
      {{ page.title }}
    {% endif %}
  {% endfor %}
