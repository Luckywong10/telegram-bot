## 介绍
纯Python异步接口Telegram Bot API，兼容Python版本**3.7+**，可作为独立包。
支持Telegram Bot API **6.6**的所有类型和方法。

基于电报的AI绘画机器人，通过`/start`指令开始运行

用户发送图片后，返回操作【服装1】【服装2】【服装3】，用户点击后，传送到后端绘画程序，绘画完成后，将图片返回给用户，扣除1积分

用户可以通过/`cz` 充值，支持usdt，支付宝充值

> 用户也可以通过分享您推广链接
> [https://t.me/xxxxxx?start=XBTUYC](https://t.me/xxxxxx?start=XBTUYC)
> 与他人一起赚钱。如果他们使用该代码在 CRYPTOBOT中进行购买，则您将从他们的每次购买中获得： 第一层用户可获得30%的返现到您的钱包中。 第二层用户可获得20%的返现到您的钱包中。 第三层用户可获得10%的返现到您的钱包中。 第四层用户可获得5% 的返现到您的钱包中。
> !!!注意：在分享之前，请先在您当前 Telegram 个人资料创建一个钱包，以便获得返现!!!

### 功能实现

-   欢迎页面：用户首次进入机器人，会看到欢迎页面，其中包含产品logo和/start指令的按钮。
-   `/开始` 指令：用户输入 `/开始` 指令，启动AI绘画机器人的功能。
-   上传图片：用户可以上传自己的图片，等待AI绘画机器人进行后续操作。
-   返回操作：上传图片后，AI绘画机器人会返回【服装1】【服装2】【服装3】的操作选项，供用户进行选择。
-   选择操作：用户可以发送图片，选择需要的操作
-   图片传输：选择操作后，AI绘画机器人会将图片传输到后端程序，进行绘画，并将绘画完成后的图片传输回给用户。
-   积分扣除：每次选择操作会扣除1积分，用户可以通过充值或邀请获取积分。
-   充值功能：用户可以通过`/充值`充值，支持Usdt（支持币安，波场）充值。
-   分享推广链接：用户可以通过分享推广链接，在其他人使用该代码购买时，获得相应的返现。
-   返现计划：`/赚钱分享` 根据购买者的层数不同，推广者可获得不同比例的返现，其中第一层用户可获得30%，第二层用户可获得20%，第三层用户可获得10%，第四层用户可获得5%的返现。
-   钱包创建：在分享之前，需要先在个`/账户中心`中创建一个钱包，以便获得返现。
-   积分管理：用户中心中增加一个积分管理功能，可以查看自己的积分余额，
-   提现：用户可以查看自己的USDT余额，并可以选择将USDT提现到自己的钱包账户中。体现需要管理员审批，提现记录及相关信息记录在数据库中。

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
我们用GPG密钥来签署所有的版本。
签名被上传到`GitHub发布页<https://github.com/python-telegram-bot/python-telegram-bot/releases>`_和`PyPI项目<https://pypi.org/project/python-telegram-bot/>`_，并以后缀`.asc`结尾。
请在<https://github.com/python-telegram-bot/python-telegram-bot/tree/master/public_keys>`_这里找到公钥。
钥匙的命名格式为``<第一个版本>-<最后一个版本>.gpg``或``<第一个版本>-当前.gpg``，如果该钥匙目前用于新版本。

此外，GitHub 发布页面还包含了后缀为``.sha1``的文件中的发布文件的 sha1 哈希值。

这使你可以验证你下载的发布文件确实是由``python-telegram-bot``团队提供的。


## 依赖&版本

尽可能少地使用第三方的依赖性，对于某些功能来说，使用第三方库比重新实现该功能更合理。
这些功能是*可选择的，因此相应的第三方依赖不被默认安装。
相反，它们被列为可选的依赖关系。
这样可以避免对不需要这些可选功能的用户产生不必要的依赖冲突。
唯一需要的依赖是 `httpx ~= 0.23.3 <https://www.python-httpx.org>`_用于
``telegram.request.HTTPXRequest``，默认网络后端。
在与其他库一起使用时最有用。
为了尽量减少依赖关系的冲突，我们在对（可选）依赖关系的版本要求方面尽量宽松。
另一方面，必须确保稳定性，这就是为什么要应用版本限制。
如果你因为这些界限而遇到了依赖性冲突，请随时联系。

## 可选依赖项
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

快速启动
===========

Our Wiki contains an `Introduction to the API <https://github.com/python-telegram-bot/python-telegram-bot/wiki/Introduction-to-the-API>`_ explaining how the pure Bot API can be accessed via ``python-telegram-bot``.
Moreover, the `Tutorial: Your first Bot <https://github.com/python-telegram-bot/python-telegram-bot/wiki/Extensions-%E2%80%93-Your-first-Bot>`_ gives an introduction on how chatbots can be easily programmed with the help of the ``telegram.ext`` module.
