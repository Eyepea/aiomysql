.. aiomysql documentation master file, created by
   sphinx-quickstart on Sun Jan 18 22:02:31 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to aiomysql's documentation!
====================================

.. _GitHub: https://github.com/aio-libs/aiomysql
.. _asyncio: http://docs.python.org/3.4/library/asyncio.html
.. _aiopg: https://github.com/aio-libs/aiopg
.. _Tornado-MySQL: https://github.com/PyMySQL/Tornado-MySQL
.. _aio-libs: https://github.com/aio-libs


**aiomysql** is a library for accessing a :term:`MySQL` database
from the asyncio_ (PEP-3156/tulip) framework. It depends and reuses most parts
of :term:`PyMySQL` . **aiomysql** try to be like awesome aiopg_ library and preserve
same api, look and feel.

Internally **aiomysql** is copy of PyMySQL, underlying io calls switched
to async, basically ``yield from`` and ``asyncio.coroutine`` added in
proper places. :term:`sqlalchemy` support ported from aiopg_.


Features
--------

- Implements *asyncio* :term:`DBAPI` *like* interface for
  :term:`MySQL`.  It includes :ref:`aiomysql-core-connection`,
  :ref:`aiomysql-core-cursor` and :ref:`aiomysql-core-pool` objects.
- Implements *optional* support for charming :term:`sqlalchemy`
  functional sql layer.

Basics
------

**aiomysql** based on :term:`PyMySQL` , and provides same api, you just need
to use  ``yield from conn.f()`` instead of just call ``conn.f()`` for
every method.

Properties are unchanged, so ``conn.prop`` is correct as well as
``conn.prop = val``.

See example:

.. code:: python

    import asyncio
    import aiomysql

    loop = asyncio.get_event_loop()

    @asyncio.coroutine
    def test_example():
        conn = yield from aiomysql.connect(host='127.0.0.1', port=3306,
                                           user='root', passwd='', db='mysql',
                                           loop=loop)

        cur = yield from conn.cursor()
        yield from cur.execute("SELECT Host,User FROM user")
        print(cur.description)
        r = yield from cur.fetchall()
        print(r)
        yield from cur.close()
        conn.close()

    loop.run_until_complete(test_example())


Installation
------------

.. code::

   pip3 install aiomysql

.. note:: :mod:`aiomysql` requires :term:`PyMySQL` library.


Also you probably want to use :mod:`aiomysql.sa`.

.. _aiomysql-install-sqlalchemy:

:mod:`aiomysql.sa` module is **optional** and requires
:term:`sqlalchemy`. You can install *sqlalchemy* by running::

  pip3 install sqlalchemy

Source code
-----------

The project is hosted on GitHub_

Please feel free to file an issue on `bug tracker
<https://github.com/aio-libs/aiomysql/issues>`_ if you have found a bug
or have some suggestion for library improvement.

The library uses `Travis <https://travis-ci.org/aio-libs/aiomysql>`_ for
Continious Integration and `Coveralls
<https://coveralls.io/r/jettify/aiomysql?branch=master>`_ for
coverage reports.


Dependencies
------------

- Python 3.3 and :mod:`asyncio` or Python 3.4+
- :term:`PyMySQL`
- aiomysql.sa requires :term:`sqlalchemy`.


Authors and License
-------------------

The ``aiomysql`` package is written by Nikolay Novik, :term:`PyMySQL` and
aio-libs_ contributors. It's MIT licensed (same as PyMySQL).

Feel free to improve this package and send a pull request to GitHub_.

Contents:
---------

.. toctree::
   :maxdepth: 2

   api
   examples
   glossary

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

