:mod:`relationlist` Changelog
================================================

:mod:`RelationList` 1.1.1
------------------------------------------------

* Fixed :meth:`related` to use the new :meth:`get_relation` instead of the old :meth:`get_relate`.

* Corrected :meth:`get_relate` and :meth:`get_relates` deprecation warning messages to show v1.4 instead of v1.2.

:mod:`Relationlist` 1.1.0
------------------------------------------------

* :meth:`repr` now returns something like :data:`RelationList(1, 2, 3)` instead of the old :data:`([1, 2, 3], [], {1: 0, 2: 0, 3: 0})`.

* :meth:`iter` now returns :data:`iter(value)` instead of :data:`iter(elm)`. Programs that need to support older versions should simply switch to :data:`iter(elm)`.

* :meth:`get_relate` is renamed to :meth:`get_relation`. The former is kept for backwards compatibility, but warns a :class:`DeprecationWarning` and will be removed in v1.4.

* :meth:`get_relates` is renamed to :meth:`get_relations`. The former is kept for backwards compatibility, but warns a :class:`DeprecationWarning` and will be removed in v1.4.

* :meth:`remove_relations` now returns a bool, :class:`False` when error suppressed by :data:`err='ignore'`, :class:`True` when no errors occured, to match :meth:`delete`.

* :meth:`get_relations` now raises :class:`ValueError` rather than :class:`KeyError` to match other methods. Programs that need to support older versions should catch both.

|

`← Main Documentation <./index.html>`_

\ \ \ `Github Pages → <./github-pages.html>`_
