reportng
========
``reportng`` is a python module to build on the fly reports.
It leverages Bootstrap 4 to automatically create using user defined bootswatch themes.
``reportng`` is capable of handling any python out including but not limited to api output, stdio output, sql queries etc.

Some example use cases of ``reportng`` are

* Create a report for a tool
* Create a report of a test
* Create a report of debugging
* etc...

``reportng`` is designed to be stackable. This means that it follows the following convention

* report_header
* report_section
* ...
* report_footer

Social
------

- `Twitter <https://twitter.com/securisec/>`_
- `Github <https://github.com/securisec/reportng>`_

Installation
------------
.. code-block:: bash

    pip install reportng

Documentation
=============

ReportWriter.__init__
---------------------
.. automethod:: reportng.ReportWriter.__init__

ReportWriter.report_header
--------------------------
.. automethod:: reportng.ReportWriter.report_header

ReportWriter.report_section
---------------------------
.. automethod:: reportng.ReportWriter.report_section

ReportWriter.report_section_collapsible
---------------------------------------
.. automethod:: reportng.ReportWriter.report_section_collapsible

ReportWriter.report_image_carousel
----------------------------------
.. automethod:: reportng.ReportWriter.report_image_carousel

ReportWriter.report_asciinema
-----------------------------
.. automethod:: reportng.ReportWriter.report_asciinema

ReportWriter.report_code_section
--------------------------------
.. automethod:: reportng.ReportWriter.report_code_section

ReportWriter.report_captions
----------------------------
.. automethod:: reportng.ReportWriter.report_captions

ReportWriter.report_table
-------------------------
.. automethod:: reportng.ReportWriter.report_table

ReportWriter.report_cards
-------------------------
.. automethod:: reportng.ReportWriter.report_cards

ReportWriter.report_footer
--------------------------
.. automethod:: reportng.ReportWriter.report_footer

ReportWriter.report_list_group
------------------------------
.. automethod:: reportng.ReportWriter.report_list_group

ReportWriter.report_section_custom_html
---------------------------------------
.. automethod:: reportng.ReportWriter.report_section_custom_html

ReportWriter.report_save
------------------------
.. automethod:: reportng.ReportWriter.report_save

.. toctree::
   :maxdepth: 2
   :caption: Contents:


Helpers
=======

JSCSS
-----
.. autoclass:: reportng.rnghelpers.JSCSS
    :members:


CSSControl
----------
.. autoclass:: reportng.rnghelpers.CSSControl
    :members:


JSCustom
--------
.. autoclass:: reportng.rnghelpers.JSCustom
    :members:


HelperFunctions
---------------
.. autoclass:: reportng.rnghelpers.HelperFunctions
    :members:


Exceptions
==========
.. autoexception:: reportng.rnghelpers.NotValidTag
.. autoexception:: reportng.rnghelpers.ObjectNotInitiated
.. autoexception:: reportng.rnghelpers.TooManyValues
.. autoexception:: reportng.rnghelpers.TableError


Example
=======

.. code-block:: python

    import reportng
    from subprocess import Popen, PIPE
    import requests

    r = reportng.ReportWriter(report_name='Demo report',
                              brand='securisec')
    report = r.report_header()

    # Multiline support
    report += r.report_section(
    'Multiline Demo',
    """
    One line
    Two line
    """)

    # Example stdio reporting
    output = Popen('ls /tmp', shell=True, stdout=PIPE).stdout.read()
    report += r.report_section('Output of ls', output,
                                tag_color='success')


    # Example using web requests
    req = requests.get('https://httpbin.org/status/418').text
    report += r.report_section('Output of requests',
                                req, tag_color='info')


    # Add an image carousel
    report += r.report_add_image_carousel(
        'foo.jpg',
        'bar.jpg',
        'baz.jpg')


    # Add description for image carousel
    report += r.report_notes('Nice pictures!')


    # Add a footer
    report += r.report_footer(message='Hello from securisec!',
                              twitter='https://twitter.com/securisec',
                              github='https://github.com/securisec')


    # Save the report!
    r.save_report(report, 'demo_report.html')


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
