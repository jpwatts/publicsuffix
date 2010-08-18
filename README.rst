============
publicsuffix
============

This module provides a Python interface to the `Public Suffix List`_.

The Public Suffix List (PSL) is a set of rules describing
"effective top-level domains" and can be used to determine the registered
domain for a given host name.

Usage
-----

The ``public_suffix_list`` function, called without arguments, will download
the PSL and return an instance of the ``SuffixList`` class containing the
current rules.

Find the registered domain::

    >>> psl = publicsuffix.public_suffix_list()
    >>> psl.domain('www.python.org')
    u'python.org'


Find the (E)TLD::

    >>> psl.tld('www.bbc.co.uk')
    u'co.uk'

    >>> psl.tld('parliament.uk')
    u'uk'


Caching
~~~~~~~

By default, ``public_suffix_list`` downloads the PSL each time it is called.
To avoid being wasteful, the function accepts optional ``http`` and
``headers`` arguments.  The object provided as ``http`` must support the
`httplib2`_ interface and will be called to download the PSL.

For example, to cache the PSL for one day::

    >>> psl = publicsuffix.public_suffix_list(
    ...     http=httplib2.Http('/path/to/cache'),
    ...     headers={'cache-control': 'max-age=%d' % (60*60*24)}
    ... )


.. _`Public Suffix List`: http://publicsuffix.org/
.. _`httplib2`: http://code.google.com/p/httplib2/
