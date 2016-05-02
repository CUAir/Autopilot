.. CUAir Autopilot Documentation documentation master file, created by
   sphinx-quickstart on Mon May  2 11:28:43 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Autopilot documentation
=========================================================

Contents:

.. toctree::
   :maxdepth: 2

   api
   groundstation

Welcome
=========

Yay, documentation!


Installation
--------------
::

   $ git clone https://github.com/CUAir/Autopilot
   $ cd Autopilot
   $ virtualenv venv 
   $ source venv/bin/activate
<<<<<<< HEAD
   $ pip install -r requirements.txt
=======
   $ pip install requirements.txt
>>>>>>> c25dde23a4f9ddcb721991222cd74831b897c3be
   $ cd docs
   $ make html


Use 
----

* To create a page, make a new file called foobar.rst. 
* Add your page to the table of contents in the file index.rst under the api and groundstation pages. 
* Edit your page using sphinx markup. 
* To see what your page looks like, compile it with ``make html``
* When you are happy with what the page looks like commit your changes with git (``git add --all; git commit -m "change message"; git push``).
* The online documentation will update sometime in the next few minutes.


To learn more about how to use sphinx, see the following guides

http://www.sphinx-doc.org/en/stable/tutorial.html

http://www.sphinx-doc.org/en/stable/rest.html#rst-primer

Support
-------

If you are having issues, please slack Troy.

License
-------
The project may or may not have a license.


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

