.. -*- rst -*-

Data types
==========

Name
----

Groonga data types

Description
-----------

Groonga identifies data types to store.

A primary key of table and column value belong to some kind of data types in Groonga database. And normally, column values become in common with all records in one table.

A primary key type and column type can be specified Groonga defined types, user defined types or user defined table.

If you specify other table to primary key type, this table becomes subset of the table of primary key type.

If you specify other table to column type, this column becomes reference key of the table of column type.

Builtin types
-------------

The following types are defined as builtin types.

.. _builtin-type-bool:

``Bool``
^^^^^^^^

Boolean type. The possible values are true and false. (default: false)

To store a value by :doc:`/reference/commands/load` command, becomes false if you specify false, 0 or empty string, becomes true if you specify others.

.. _builtin-type-int8:

``Int8``
^^^^^^^^

Signed 8bit integer. It's -128 or more and 127 or less. (default: 0)

.. _builtin-type-uint8:

``UInt8``
^^^^^^^^^

Unsigned 8bit integer. Is't 0 or more and 255 or less. (default: 0)

.. _builtin-type-int16:

``Int16``
^^^^^^^^^

Signed 16bit integer. It's -32,768 or more and 32,767 or less. (default: 0)

.. _builtin-type-uint16:

``UInt16``
^^^^^^^^^^

Unsigned 16bit integer. It's 0 or more and 65,535 or less. (default: 0)

.. _builtin-type-int32:

``Int32``
^^^^^^^^^

Signed 32bit integer. It's -2,147,483,648 or more and 2,147,483,647 or less. (default: 0)

.. _builtin-type-uint32:

``UInt32``
^^^^^^^^^^

Unsigned 32bit integer. It's 0 or more and 4,294,967,295 or less. (default: 0)

.. _builtin-type-int64:

``Int64``
^^^^^^^^^

Signed 64bit integer. It's -9,223,372,036,854,775,808 or more and 9,223,372,036,854,775,807 or less. (default: 0)

.. _builtin-type-uint64:

``UInt64``
^^^^^^^^^^

Unsigned 64bit integer. It's 0 or more and 18,446,744,073,709,551,615 or less. (default: 0)

.. _builtin-type-float:

``Float32``
^^^^^^^^^^^

.. versionadded:: 10.0.2

Single-precision floating-point number of IEEE 754 as a real number. (default: 0.0)

See `IEEE floating point - Wikipedia, the free encyclopedia <http://en.wikipedia.org/wiki/IEEE_floating_point>`_ or `IEEE 754: Standard for Binary Floating-Point <http://grouper.ieee.org/groups/754/>`_ for details of IEEE 754 format.

``Float``
^^^^^^^^^

Double-precision floating-point number of IEEE 754 as a real number. (default: 0.0)

See `IEEE floating point - Wikipedia, the free encyclopedia <http://en.wikipedia.org/wiki/IEEE_floating_point>`_ or `IEEE 754: Standard for Binary Floating-Point <http://grouper.ieee.org/groups/754/>`_ for details of IEEE 754 format.

.. _builtin-type-time:

``Time``
^^^^^^^^

Date and Time, the number of seconds that have elapsed since 1970-01-01 00:00:00 by 64 bit signed integer. (default: 0)

To store a value by :doc:`/reference/commands/load` command, specifies the number of elapsed seconds since 1970-01-01 00:00:00. To specify the detailed date and time than seconds, use the decimal.

.. _builtin-type-short-text:

``ShortText``
^^^^^^^^^^^^^

String of 4,095 or less bytes. (default: "")

.. _builtin-type-text:

``Text``
^^^^^^^^

String of 65,535 or less bytes. (default: "")

.. _builtin-type-long-text:

``LongText``
^^^^^^^^^^^^

String of 2,147,483,647 or less bytes. (default: "")

.. _builtin-type-tokyo-geo-point:

``TokyoGeoPoint``
^^^^^^^^^^^^^^^^^

Represent longitude and latitude by set of integer representing in millisecond. The longtitude and latitude of TokyoGeoPoint are based on old Japanese Geodetic datum. (default: "0x0") 
Longititude and latitude displayed as X degree Y minutes Z second will be converted to millisecond unit with following caliculation (((X * 60) + Y) * 60 + Z) * 1000.

Use text string ``Longitude in millisecond unit x Latitude in milliscond unit`` or ``Latitude in a decimal x Longititude in a decimal`` to store value with :doc:`/reference/commands/load` command.``x`` and``,`` would be used as separator for longitude and latitude. 


For more details about Geodatic datum, refer to `Geodatic datum - Wikipedia <https://en.wikipedia.org/wiki/Geodetic_datum>`

.. _builtin-type-wgs84-geo-point:

``WGS84GeoPoint``
^^^^^^^^^^^^^^^^^

Longtitude and latitude based on World Geodetic System, WGS 84. Longtitudeand latitude are displayed by set unit of integer representing millisecond. (default: "0x0") 

Conversion method into millisecond and command methods of :doc:`/reference/commands/load` are same as TokyoGeoPoint. 

Limitations about types
-----------------------

Types that can't be specified in primary key of table
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``Text`` and ``LongText`` can't be specified in primary key of table.

ベクターとして格納できない型
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Groongaのカラムは、ある型のベクターを保存することができます。しかし、ShortText, Text, LongTextの３つの型についてはベクターとして保存したり出力したりすることはできますが、検索条件やドリルダウン条件に指定することができません。

テーブル型は、ベクターとして格納することができます。よって、ShortTextのベクターを検索条件やドリルダウン条件に使用したい場合には、主キーがShortText型のテーブルを別途作成し、そのテーブルを型として利用します。
