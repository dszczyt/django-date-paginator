What is more stupid than paginating your objects by an arbitrary number per page ?
So I created this peace of code for paginating objects by date. Easy, fast, efficient and very user friendly. The essential tool for your Django project.


---

# Getting Started #
First, you should fetch the code in your root directory... See the [source page](http://code.google.com/p/django-date-paginator/source/checkout). Add date\_paginator in your settings apps.
## Set up your urls.py ##
Your urls.py should contain a parameter "selector".
Sample :
```
...
url(r'^list/(?P<selector>[^/]*)/$', 'object_list', name = 'object_list_paginated'),
...
```
## Set up your views.py ##
First import the project :
```
from date_paginator.DatePaginator import DatePaginator
```
Considering you want to paginate with the attribute "creation\_date" which is a DateField in your MyObject model, you can write this view :
```
def object_list(request, selector):
    objects = DatePaginator(MyObject.objects.all(), 'creation_date', 'object_list_paginated').page(selector)
    return render_to_response("object_list.html",
                              {
                                 "objects": objects
                              }
                             )
```
## Set up your templates ##
You can access your objects with _objects.object\_list_ .
To insert navigation items :
```
{% include "date_paginator.html" %}
```
By default, you've got access to the 60 first elements. Create a link to the next page with :
```
{% if products.has_more %}
<div class="more_objects">
    <a href="{{ objects.next_page.get_absolute_url }}">
        {{ objects.remaining_objects }} more objects...
    </a>
</div>
{% endif %}
```

---

Enjoy !!