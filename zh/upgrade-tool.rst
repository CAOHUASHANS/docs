升级工具
############

CakePHP 2.x 升级到 CakePHP 3 需要做一些列的操作，但是这些操作大部分都可以自动化实现，例如增加命名空间。
为了使这些机械性的升级操作简单些，CakePHP 在升级工具的基础上，提供了一个CLI命令。


安装
============
升级工具是作为一个独立的应用安装的，需要使用git工具克隆一份升级工具包，并且使用composer工具安装先关依赖::

    git clone https://github.com/cakephp/upgrade.git
    cd upgrade
    php ../composer.phar install

此时，你应该能够获得升级工具的帮助::

    cd upgrade
    bin/cake upgrade --help

上面的命令输出结果如下::

    Welcome to CakePHP v3.0.8 Console
    ---------------------------------------------------------------
    App : src
    Path: /Users/markstory/Sites/cake_plugins/upgrade/src/
    ---------------------------------------------------------------
    A shell to help automate upgrading from CakePHP 2.x to 3.x. Be sure to
    have a backup of your application before running these commands.

    Usage:
    cake upgrade [subcommand] [-h] [-v] [-q]

    Subcommands:

    locations           Move files/directories around. Run this *before*
                        adding namespaces with the namespaces command.
    namespaces          Add namespaces to files based on their file path.
                        Only run this *after* you have moved files.
    app_uses            Replace App::uses() with use statements
    rename_classes      Rename classes that have been moved/renamed. Run
                        after replacing App::uses() with use statements.
    rename_collections  Rename HelperCollection, ComponentCollection, and
                        TaskCollection. Will also rename component
                        constructor arguments and _Collection properties on
                        all objects.
    method_names        Update many of the methods that were renamed during
                        2.x -> 3.0
    method_signatures   Update many of the method signatures that were
                        changed during 2.x -> 3.0
    fixtures            Update fixtures to use new index/constraint
                        features. This is necessary before running tests.
    tests               Update test cases regarding fixtures.
    i18n                Update translation functions regarding placeholders.
    skeleton            Add basic skeleton files and folders from the "app"
                        repository.
    prefixed_templates  Move view templates for prefixed actions.
    all                 Run all tasks expect for skeleton. That task should
                        only be run manually, and only for apps (not
                        plugins).

    To see help on a subcommand use `cake upgrade [subcommand] --help`

    Options:

    --help, -h     Display this help.
    --verbose, -v  Enable verbose output.
    --quiet, -q    Enable quiet output.

使用方法
=====

一旦正确安装了升级工具，升级一个 CakePHP 2.x 项目的准备就已经做好了

.. 注意 ::
    确保你的应用程序代码具有备份/版本控制。
    
    建议你在每个子命令之后做备份/提交。

开始运行``locations`` 命令::

    # 查看命令的选项
    bin/cake upgrade locations --help

    # 在 dry mode 模式下运行命令
    bin/cake upgrade locations --dry-run /path/to/app

在 dry mode 模式下运行的输出告诉你，当命令真正执行之后将会发生哪些改变。如果你想真正执行以上命令，去掉命令行里面的``--dry-run``参数即可。
也可以通过增加``--git``参数，可以自动移动Git中的文件。

Once file locations have been updated, you can add namespaces to your code using
一旦更新了文件位置，就可以在代码中添加命名空间了。
使用 ``namespaces`` 命令::

    # 查看命令的选项
    bin/cake upgrade namespaces --help

    # 在 dry mode 模式下运行命令
    bin/cake upgrade namespaces --dry-run /path/to/app

    # 运行真实的命令
    bin/cake upgrade namespaces /path/to/app

在这两个命令之后，你可以按照任何顺序执行余下的子命令了。
