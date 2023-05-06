## 介绍
纯Python异步接口Telegram Bot API，兼容Python版本**3.7+**，可作为独立包。
支持Telegram Bot API **6.6**的所有类型和方法。

## 安装
You can install or upgrade ``python-telegram-bot`` via

.. code:: shell

    $ pip install python-telegram-bot --upgrade

To install a pre-release, use the ``--pre`` `flag <https://pip.pypa.io/en/stable/cli/pip_install/#cmdoption-pre>`_ in addition.

You can also install ``python-telegram-bot`` from source, though this is usually not necessary.

.. code:: shell

    $ git clone https://github.com/python-telegram-bot/python-telegram-bot
    $ cd python-telegram-bot
    $ python setup.py install

## 版本验证
We sign all the releases with a GPG key.
The signatures are uploaded to both the `GitHub releases page <https://github.com/python-telegram-bot/python-telegram-bot/releases>`_ and the `PyPI project <https://pypi.org/project/python-telegram-bot/>`_ and end with a suffix ``.asc``.
Please find the public keys `here <https://github.com/python-telegram-bot/python-telegram-bot/tree/master/public_keys>`_.
The keys are named in the format ``<first_version>-<last_version>.gpg`` or ``<first_version>-current.gpg`` if the key is currently being used for new releases.

In addition, the GitHub release page also contains the sha1 hashes of the release files in the files with the suffix ``.sha1``.

This allows you to verify that a release file that you downloaded was indeed provided by the ``python-telegram-bot`` team.

## Dependencies & Their Versions

``python-telegram-bot`` tries to use as few 3rd party dependencies as possible.
However, for some features using a 3rd party library is more sane than implementing the functionality again.
As these features are *optional*, the corresponding 3rd party dependencies are not installed by default.
Instead, they are listed as optional dependencies.
This allows to avoid unnecessary dependency conflicts for users who don't need the optional features.

The only required dependency is `httpx ~= 0.23.3 <https://www.python-httpx.org>`_ for
``telegram.request.HTTPXRequest``, the default networking backend.

``python-telegram-bot`` is most useful when used along with additional libraries.
To minimize dependency conflicts, we try to be liberal in terms of version requirements on the (optional) dependencies.
On the other hand, we have to ensure stability of ``python-telegram-bot``, which is why we do apply version bounds.
If you encounter dependency conflicts due to these bounds, feel free to reach out.

## Optional Dependencies
PTB can be installed with optional dependencies:

* ``pip install python-telegram-bot[passport]`` installs the `cryptography>=39.0.1 <https://cryptography.io/en/stable>`_ library. Use this, if you want to use Telegram Passport related functionality.
* ``pip install python-telegram-bot[socks]`` installs `httpx[socks] <https://www.python-httpx.org/#dependencies>`_. Use this, if you want to work behind a Socks5 server.
* ``pip install python-telegram-bot[http2]`` installs `httpx[http2] <https://www.python-httpx.org/#dependencies>`_. Use this, if you want to use HTTP/2.
* ``pip install python-telegram-bot[rate-limiter]`` installs `aiolimiter~=1.0.0 <https://aiolimiter.readthedocs.io/en/stable/>`_. Use this, if you want to use ``telegram.ext.AIORateLimiter``.
* ``pip install python-telegram-bot[webhooks]`` installs the `tornado~=6.2 <https://www.tornadoweb.org/en/stable/>`_ library. Use this, if you want to use ``telegram.ext.Updater.start_webhook``/``telegram.ext.Application.run_webhook``.
* ``pip install python-telegram-bot[callback-data]`` installs the `cachetools~=5.3.0 <https://cachetools.readthedocs.io/en/latest/>`_ library. Use this, if you want to use `arbitrary callback_data <https://github.com/python-telegram-bot/python-telegram-bot/wiki/Arbitrary-callback_data>`_.
* ``pip install python-telegram-bot[job-queue]`` installs the `APScheduler~=3.10.1 <https://apscheduler.readthedocs.io/en/3.x/>`_ library and enforces `pytz>=2018.6 <https://pypi.org/project/pytz/>`_, where ``pytz`` is a dependency of ``APScheduler``. Use this, if you want to use the ``telegram.ext.JobQueue``.

To install multiple optional dependencies, separate them by commas, e.g. ``pip install python-telegram-bot[socks,webhooks]``.

Additionally, two shortcuts are provided:

* ``pip install python-telegram-bot[all]`` installs all optional dependencies.
* ``pip install python-telegram-bot[ext]`` installs all optional dependencies that are related to ``telegram.ext``, i.e. ``[rate-limiter, webhooks, callback-data, job-queue]``.

Quick Start
===========

Our Wiki contains an `Introduction to the API <https://github.com/python-telegram-bot/python-telegram-bot/wiki/Introduction-to-the-API>`_ explaining how the pure Bot API can be accessed via ``python-telegram-bot``.
Moreover, the `Tutorial: Your first Bot <https://github.com/python-telegram-bot/python-telegram-bot/wiki/Extensions-%E2%80%93-Your-first-Bot>`_ gives an introduction on how chatbots can be easily programmed with the help of the ``telegram.ext`` module.

Resources
=========

- The `package documentation <https://docs.python-telegram-bot.org/>`_ is the technical reference for ``python-telegram-bot``.
  It contains descriptions of all available classes, modules, methods and arguments as well as the `changelog <https://docs.python-telegram-bot.org/changelog.html>`_.
- The `wiki <https://github.com/python-telegram-bot/python-telegram-bot/wiki/>`_ is home to number of more elaborate introductions of the different features of ``python-telegram-bot`` and other useful resources that go beyond the technical documentation.
- Our `examples section <https://docs.python-telegram-bot.org/examples.html>`_ contains several examples that showcase the different features of both the Bot API and ``python-telegram-bot``.
  Even if it is not your approach for learning, please take a look at ``echobot.py``. It is the de facto base for most of the bots out there.
  The code for these examples is released to the public domain, so you can start by grabbing the code and building on top of it.
- The `official Telegram Bot API documentation <https://core.telegram.org/bots/api>`_ is of course always worth a read.

Getting help
============

If the resources mentioned above don't answer your questions or simply overwhelm you, there are several ways of getting help.

1. We have a vibrant community of developers helping each other in our `Telegram group <https://telegram.me/pythontelegrambotgroup>`_. Join us! Asking a question here is often the quickest way to get a pointer in the right direction.

2. Ask questions by opening `a discussion <https://github.com/python-telegram-bot/python-telegram-bot/discussions/new>`_.

3. You can even ask for help on Stack Overflow using the `python-telegram-bot tag <https://stackoverflow.com/questions/tagged/python-telegram-bot>`_.

Concurrency
===========

Since v20.0, ``python-telegram-bot`` is built on top of Pythons ``asyncio`` module.
Because ``asyncio`` is in general single-threaded, ``python-telegram-bot`` does currently not aim to be thread-safe.
Noteworthy parts of ``python-telegram-bots`` API that are likely to cause issues (e.g. race conditions) when used in a multi-threaded setting include:

* ``telegram.ext.Application/Updater.update_queue``
* ``telegram.ext.ConversationHandler.check/handle_update``
* ``telegram.ext.CallbackDataCache``
* ``telegram.ext.BasePersistence``
* all classes in the ``telegram.ext.filters`` module that allow to add/remove allowed users/chats at runtime

Contributing
============

Contributions of all sizes are welcome.
Please review our `contribution guidelines <https://github.com/python-telegram-bot/python-telegram-bot/blob/master/.github/CONTRIBUTING.rst>`_ to get started.
You can also help by `reporting bugs or feature requests <https://github.com/python-telegram-bot/python-telegram-bot/issues/new>`_.

Donating
========
Occasionally we are asked if we accept donations to support the development.
While we appreciate the thought, maintaining PTB is our hobby, and we have almost no running costs for it. We therefore have nothing set up to accept donations.
If you still want to donate, we kindly ask you to donate to another open source project/initiative of your choice instead.

License
=======

You may copy, distribute and modify the software provided that modifications are described and licensed for free under `LGPL-3 <https://www.gnu.org/licenses/lgpl-3.0.html>`_.
Derivatives works (including modifications or anything statically linked to the library) can only be redistributed under LGPL-3, but applications that use the library don't have to be.
