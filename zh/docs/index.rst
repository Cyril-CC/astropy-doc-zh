.. Astropy documentation master file, created by
   sphinx-quickstart on Tue Jul 26 02:59:34 2011.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

:tocdepth: 3

.. the "raw" directive below is used to hide the title in favor of just the logo being visible
.. raw:: html

    <style media="screen" type="text/css">
      h1 { display:none; }
    </style>

#####################
Astropy 文档
#####################

.. |logo_svg| image:: _static/astropy_banner.svg

.. |logo_png| image:: _static/astropy_banner_96.png

.. raw:: html

   <img src="_images/astropy_banner.svg" onerror="this.src='_images/astropy_banner_96.png'; this.onerror=null;" width="485"/>

.. only:: latex

    .. image:: _static/astropy_logo.pdf

``astropy`` 包含了用Python实现的实行天文学和天体物理学所需的关键功能与常用工具.

它是 `Astropy项目 <http://www.astropy.org/about.html>`_ 的核心, 旨在使社区能够建立一个鲁棒的 `附属包 <http://www.astropy.org/affiliated/index.html>`_ 系统, 满足天文研究, 数据处理和数据分析的需求.

.. _getting-started:

***************
入门
***************

.. toctree::
   :maxdepth: 1

   install
   whatsnew/3.1
   importing_astropy
   Example Gallery <generated/examples/index>
   Tutorials <http://tutorials.astropy.org/>
   Get Help <http://www.astropy.org/help.html>
   Contribute and Report Problems <http://www.astropy.org/contribute.html>
   About the Astropy Project <http://www.astropy.org/about.html>

.. _user-docs:

******************
用户文档
******************

数据结构与转换
-----------------------------------

.. toctree::
   :maxdepth: 1

   constants/index
   units/index
   nddata/index
   table/index
   time/index
   coordinates/index
   wcs/index
   modeling/index

文件, I/O, 和交互
-----------------------------

.. toctree::
   :maxdepth: 1

   io/unified
   io/fits/index
   io/ascii/index
   io/votable/index
   io/misc
   samp/index

计算与作用
--------------------------

.. toctree::
   :maxdepth: 1

   cosmology/index
   convolution/index
   visualization/index
   stats/index

核心与部件
--------------

.. toctree::
   :maxdepth: 1

   config/index
   io/registry
   logging
   warnings
   utils/index
   testhelpers
   development/workflow/get_devel_version

.. _developer-docs:

=======================
开发者文档
=======================

开发人员文档包含了关于如何为Astropy及其附属软件包做出贡献的说明, 以及其编码, 文档和测试指南.
对于开发过程与整个项目, 参见 :doc:`development/vision`.

.. toctree::
   :maxdepth: 1

   development/workflow/development_workflow
   development/when_to_rebase
   development/codeguide
   development/docguide
   development/testguide
   development/scripts
   development/building
   development/ccython
   development/releasing
   development/workflow/maintainer_workflow
   development/astropy-package-template
   changelog

还有一些维护者使用的工具, 在常用天文Python包建议 <https://github.com/astropy/astropy-procedures>`__ 中.

.. _project-details:

***************
项目详情
***************

.. toctree::
   :maxdepth: 1

   stability
   whatsnew/index
   known_issues
   credits
   license

*****
索引
*****

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

.. _feedback@astropy.org: mailto:feedback@astropy.org
