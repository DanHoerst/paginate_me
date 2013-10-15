paginate_me
===========

An easy utility I use for pagination in Django.

Implementation - 

1) Move the paginate folder into your Django project.

2) Use paginate_me() in your project. 

Example - 

The paginate_me() function takes 3 values - the request, the queryset of values you want paginated, and the amount of values you want on each page.
It returns two values, the iterable listing and the iterable for the pagination.

views.py:

    from paginate_me.paginate import paginate_me

    list_of_values = Lists.objects.filter(user=request.user)
    listing, paginator = paginate_me(request, list_of_values, 6)


templates.html:

    <div class="pagination">
        <ul>
            <li {% if not listing.has_previous %}class="disabled"{% endif %}><a class="navlink" href="?page={% if listing.has_previous %}{{ listing.previous_page_number }}{% endif %}"><span>Prev</span></a></li>
            {% for page in paginator.page_range %}
                <li {% if listing.number == page %}class="active"{% endif %}><a href="?page={{ page }}"><span>{{ page }}</span></a></li>
            {% endfor %}
            <li {% if not listing.has_next %}class="disabled"{% endif %}><a class="navlink" href="?page={% if listing.has_next %}{{ listing.next_page_number }}{% endif %}"><span>Next</span></a></li>
        </ul>
    </div>
