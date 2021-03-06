----------------------------------------
Samurai Payment Integration
----------------------------------------

`Samurai  Payment Integration`_ is a service offered by 
`FeeFighters`_ to reduce the complexity of PCI compliance.

.. note::

   This integration makes use of the official `samurai`_ python package offered
   by Samurai  Payments. Please install it before you use this integration.

Settings attributes required for this integration are:



Here are the methods and attributes implemented on the ``SamuraiIntegration`` class:

* ``__init__(self, options=None)``: The constructor method 

* ``get_urls(self)``: The method sets the url to which the token is sent
  after the it is obtained from Samurai. This method is generally mapped 
  directly in the ``urls.py``.

  .. code::

     from billing import get_integration

     samurai = get_integration("samurai")

     urlpatterns += patterns('',
        (r'^samurai/', include(samurai_obj.urls)),
     )

* ``get_token(self, request)``: The view method that recieves the
token   

* ``generate_form(self)``: The method that generates and returns the form (present in 
  ``billing.forms.samurai_forms``) 


Example:
--------

    In the views.py::

       samurai_obj = get_integration("samurai")
       return render_to_response("some_template.html", 
                               {"samurai_obj": samurai_obj},
                                context_instance=RequestContext(request))

   In the urls.py::

      samurai_obj = get_integration("samurai")
      urlpatterns += patterns('',
         (r'^samurai/', include(samurai_obj.urls)),
      )
      
   In the template::

      {% load billing_tags %}

      {% samurai_payment samurai_obj %}


.. _`Samurai Payment`: https://samurai.feefighters.com/
.. _`samurai`: http://pypi.python.org/pypi/samurai/0.6
.. _`FeeFighters`: http://feefighters.com/
