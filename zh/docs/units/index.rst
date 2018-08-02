.. _astropy-units:

**************************************
Units and Quantities (`astropy.units`)
**************************************

.. |quantity| replace:: :class:`~astropy.units.Quantity`

.. currentmodule:: astropy.units

简介
============

`astropy.units` 可以对如米, 秒, 赫兹等物理量进行定义, 转换和执行计算. 它还处理对数单位，如幅度和分贝。

`astropy.units` 不能处理球形几何或六十进制(小时, 分钟, 秒) : 如果你想处理天体坐标, 请参阅 `astropy.coordinates` 包.

入门
===============

大多数使用 `astropy.units` 包的用户将会 :ref:`使用 "quantities"
<quantity>`:值和单位的组合.  
The easiest way to create
创建一个 |quantity| 的最简单的方法是, 用一个值乘以或除以一个内置单位.
它适用于标量, 序列和Numpy数组::

    >>> from astropy import units as u
    >>> 42.0 * u.meter  # doctest: +FLOAT_CMP
    <Quantity  42. m>
    >>> [1., 2., 3.] * u.m  # doctest: +FLOAT_CMP
    <Quantity [1., 2., 3.] m>
    >>> import numpy as np
    >>> np.array([1., 2., 3.]) * u.m  # doctest: +FLOAT_CMP
    <Quantity [1., 2., 3.] m>

您也可从 |quantity| 中获取其的值和单位等::

    >>> q = 42.0 * u.meter
    >>> q.value
    42.0
    >>> q.unit
    Unit("m")

由这个简单的构建模块, 您可以很容易将值与不同单位组合在一起 ::

    >>> 15.1 * u.meter / (32.0 * u.second)  # doctest: +FLOAT_CMP
    <Quantity 0.471875 m / s>
    >>> 3.0 * u.kilometer / (130.51 * u.meter / u.second)  # doctest: +FLOAT_CMP
    <Quantity 0.022986744310780783 km s / m>
    >>> (3.0 * u.kilometer / (130.51 * u.meter / u.second)).decompose()  # doctest: +FLOAT_CMP
    <Quantity 22.986744310780782 s>

单位转换使用了
:meth:`~astropy.units.quantity.Quantity.to` 方法, 返回了一个单位为给定单位的新的 |quantity| 对象::

    >>> x = 1.0 * u.parsec
    >>> x.to(u.km)  # doctest: +FLOAT_CMP
    <Quantity 30856775814671.914 km>

其也可以直接与较低级别的单位一同使用, 例如, 创建自定义单位::

    >>> from astropy.units import imperial

    >>> cms = u.cm / u.s
    >>> # ...and then use some imperial units
    >>> mph = imperial.mile / u.hour

    >>> # And do some conversions
    >>> q = 42.0 * cms
    >>> q.to(mph)  # doctest: +FLOAT_CMP
    <Quantity 0.939513242662849 mi / h>

"抵消" 是一个特殊的单位，称为 "无量纲单位":

    >>> u.m / u.m
    Unit(dimensionless)

`astropy.units` 能将符合单位与其内置的单位进行匹配::

    >>> (u.s ** -1).compose()  # doctest: +SKIP
    [Unit("Bq"), Unit("Hz"), Unit("3.7e+10 Ci")]

它也可以在单位制之间进行转换, 例如 SI 或 CGS:

.. doctest-skip::

    >>> (1.0 * u.Pa).cgs
    <Quantity 10.0 Ba>

特殊单位 ``mag``, ``dex`` 和 ``dB`` , 是 :ref:`对数单位 <logarithmic_units>`, 其值是给定单位中物理量的对数.  这些可以与括号中的一个物理单位创建其对应的对数值::

    >>> -2.5 * u.mag(u.ct / u.s)
    <Magnitude -2.5 mag(ct / s)>
    >>> from astropy import constants as c
    >>> u.Dex((c.G * u.M_sun / u.R_sun**2).cgs)  # doctest: +FLOAT_CMP
    <Dex 4.438067627303133 dex(cm / s2)>

`astropy.units` 也能进行 :ref:`单位换算公式 <unit_equivalencies>`, 例如波长与频率之间的换算.

在使用该功能, 换算对象传递给 :meth:`~astropy.units.quantity.Quantity.to` 转换方法. 
譬如, 从波长到频率的转换通常是不能进行的:

    >>> (1000 * u.nm).to(u.Hz)  # doctest: +IGNORE_EXCEPTION_DETAIL
    Traceback (most recent call last):
      ...
    UnitConversionError: 'nm' (length) and 'Hz' (frequency) are not convertible

但通过传递一个等价列表, 在这个情况下 ``spectral()``, 它能进行:

    >>> (1000 * u.nm).to(u.Hz, equivalencies=u.spectral())  # doctest: +FLOAT_CMP
    <Quantity  2.99792458e+14 Hz>

使用 `格式字符串语法
<https://docs.python.org/3/library/string.html#format-string-syntax>`_ 可以将数量和单位 :ref:`很好地打印成字符串
<astropy-units-format>` , 是最新版本的 python 中的字符串格式化语法. 
格式说明符 (如 ``0.03f``) in new-style 在新的格式字符串中将用于格式化数量值::

    >>> q = 15.1 * u.meter / (32.0 * u.second)
    >>> q  # doctest: +FLOAT_CMP
    <Quantity 0.471875 m / s>
    >>> "{0:0.03f}".format(q)
    '0.472 m / s'

其也可以单独格式化值和单位. 格式化说明符可以用于选择单位格式化::

    >>> q = 15.1 * u.meter / (32.0 * u.second)
    >>> q  # doctest: +FLOAT_CMP
    <Quantity 0.471875 m / s>
    >>> "{0.value:0.03f} {0.unit:FITS}".format(q)
    '0.472 m s-1'

使用 `astropy.units`
=====================

.. toctree::
   :maxdepth: 2

   quantity
   standard_units
   combining_and_defining
   decomposing_and_composing
   logarithmic_units
   format
   equivalencies
   conversion

其他
========

- `FITS标准 <https://fits.gsfc.nasa.gov/fits_standard.html>`_ 参见FIST部分.

- `VO 1.0标准
  <http://www.ivoa.net/Documents/VOUnits/>`_ 用于代表VO中的部分.

- OGIP : 一个用于 `OGIP FITS文件
  <https://heasarc.gsfc.nasa.gov/docs/heasarc/ofwg/docs/general/ogip_93_001/>`_中存储单元标准.

- `天文目录单位的标准
  <http://cds.u-strasbg.fr/doc/catstd-3.2.htx>`_.

- `IAU 主题手册
  <https://www.iau.org/static/publications/stylemanual1989.pdf>`_.

- `天文单位换算表
  <http://www.stsci.edu/~strolger/docs/UNITS.txt>`_

.. note that if this section gets too long, it should be moved to a separate 
   doc page - see the top of performance.inc.rst for the instructions on how to do 
   that
.. include:: performance.inc.rst

Reference/API
=============

.. automodapi:: astropy.units.quantity

.. automodapi:: astropy.units

.. automodapi:: astropy.units.format

.. automodapi:: astropy.units.si

.. automodapi:: astropy.units.cgs

.. automodapi:: astropy.units.astrophys

.. automodapi:: astropy.units.function.units

.. automodapi:: astropy.units.imperial

.. automodapi:: astropy.units.cds

.. automodapi:: astropy.units.equivalencies

.. automodapi:: astropy.units.function

.. automodapi:: astropy.units.deprecated

.. automodapi:: astropy.units.required_by_vounit

致谢
===============

这部分代码改编自Andrew Pontzen编写的 `pynbody
<https://github.com/pynbody/pynbody>`模块, 他已授予Astropy项目使用BSD lic下的代码的权限.