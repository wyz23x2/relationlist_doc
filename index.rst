:mod:`relationlist` Documentation
================================================

.. module:: relationlist

What is :class:`relationlist`?

Sometimes we want more from :class:`list`. Say you have elements :data:`1` and :data:`4`. You want to assign :data:`5` to the values, but don't want a :class:`dict` or something like :data:`[(1, 4, 5)]`. :class:`relationlist` is here to help you.

_________________________________________________

Installing is easy. Run this in the command line:

``$ python3 -m pip install relationlist``

Or this in shell:

.. code:: python
>>> __import__('os').system('python3 -m pip install relationlist')

After that, test it:

.. code:: python
>>> import relationlist
>>> # You're ready to use relationlist!

_________________________________________________

.. class:: RelationList(iterable=(), /)

    A class that supports relations.

    *iterable*: An iterable that is converted into a :class:`list` and stored in :attr:`value`.

    .. versionchanged:: 1.1.0
       The *lis* parameter is renamed to *iterable* and accepts any iterable.
    .. versionchanged:: 1.1.0
       The default value is changed to an empty :class:`tuple` instead of :class:`None` to reflect defaults of :class:`list()` and :class:`tuple()`.
    .. .. versionchanged:: 1.1.1
    .. :class:`DeprecationWarning` is raised when :class:`None` is passed to set :attr:`value` to :data:`[]`. It will be invalid starting from v1.2.

These are the instances of :class:`RelationList`:

.. method:: RelationList.add(val, /, index=-1)

    Inserts *val* to the index given. Equal to :meth:`list.insert`/:meth:`list.append`.

.. method:: RelationList.clear_relations()

    Clears all relations.

.. method:: RelationList.erase_relations()

    Alias of :meth:`clear_relations()`.

.. method:: RelationList.copy(*, deep=True)

    Returns :meth:`copy.deepcopy` if *deep*, or else :meth:`copy.copy`.

.. method:: RelationList.delete(val, /, *, error='raise') -> bool

    Deletes *val* from :attr:`value`.

    :data:`error='raise'`: :class:`ValueError` is raised when *val* is not in :attr:`value`.

    :data:`error='ignore'`: The error is suppressed, and :class:`False` is returned.

    :class:`True` is returned when the error is not raised or suppressed.

.. attribute:: RelationList.elm

    A :class:`dict` that contains count of relations for values in :attr:`value`.

.. method:: RelationList.generator(*, func=False)

    If :data:`func` is :class:`False`, returns a generator of :attr:`value`, else returns a function that returns the generator when called.

.. method:: RelationList.get_relation(val1, val2, /) -> tuple

    Returns a :class:`tuple` of the form :data:`(val1, val2, mode, assignment)` representing the relation between *val1* and *val2*. Raises :class:`ValueError` apon failure.

    .. versionchanged:: 1.1.0
       :meth:`get_relate` is renamed to :meth:`get_relation`. The former is kept for backwards compatibility, but warns a :class:`DeprecationWarning` and will be removed in v1.4.


.. method:: RelationList.get_relations(key, /) -> list

    Returns a :class:`list` that contains all relations related to *key* in a :class:`tuple` of the form :data:`(val1, val2, mode, assignment)`. Raises :class:`ValueError` apon failure.

    .. versionchanged:: 1.1.0
       :class:`ValueError` is raised rather than :class:`KeyError` to match other methods. Programs that need to support v1.0 and newer should catch both.

    .. versionchanged:: 1.1.0
       :meth:`get_relates` is renamed to :meth:`get_relations`. The former is kept for backwards compatibility, but warns a :class:`DeprecationWarning` and will be removed in v1.4.

.. method:: RelationList.relate(val1, val2, /, mode='break', assignment=None)

    Creates a relation between *val1* and *val2*.

    *mode*: :data:`'break'` or :data:`'delete'`.

        :data:`mode='break'`: When *val1* or *val2* is deleted, the relation is deleted. The other value will not be affected.

        :data:`mode='delete'`: When *val1* or *val2* is deleted, the relation is deleted. The other value will be deleted together.

    *assignment*: Assign a value to the relation, default :class:`None`.

.. method:: RelationList.relate_all(mode='break', assignments=None)

    Creates relations between all elements.

    *mode*: See :meth:`relate()` for information.

    *assignments*: If not an iterable, assigned to all relations. If is, :data:`assignments[order]` is assigned to each relation. The last element will be used if :class:`IndexError` occurs.

    Order (:data:`value=[1, 2, 3] assignments=[4, 5, 6]`):

    1↔2: 4 |
    1↔3: 5 |
    2↔3: 6

.. method:: RelationList.related(val1, val2, /) -> bool

   Checks if *val1* and *val2* are related.
   
   .. versionchanged:: 1.1.1
      :meth:`related` now uses the new :meth:`get_relation` instead of the old :meth:`get_relate`.

.. attribute:: RelationList.relations

   Returns a :class:`list` that contains all relations in a :class:`tuple` of the form :data:`(val1, val2, mode, assignment)`.

.. method:: RelationList.remove_relation(val1, val2, /) -> bool

   Deletes the relation from :attr:`value`.

    :data:`error='raise'`: :class:`ValueError` is raised when *val1* and *val2* are not related.

    :data:`error='ignore'`: The error is suppressed, and :class:`False` is returned.

    :class:`True` is returned when the error is not raised or suppressed.

   .. versionchanged:: 1.1.0
      A :class:`bool` is returned instead of :class:`None` to match :meth:`delete`.

.. attribute:: RelationList.value

   Returns the base :class:`list` in the class. Note changes to this will not effect the one inside.

.. method:: RelationList.__add__(other)

   Called with :data:`self + other`.

   If *other* is a :class:`RelationList`, returns a deepcopy of :class:`self` that :attr:`__iadd__` s *other*.

   If *other* is a :class:`list`, returns returns a deepcopy of :class:`self` that extended :attr:`value` with *other*.

.. method:: RelationList.__radd__(other)

   Called with :data:`list + self`.

   Same as :meth:`__add__`, but the :class:`list` is inserted before :attr:`value`.

.. method:: RelationList.__iadd__(other)

   Called with :data:`self += other`.

   If *other* is a :class:`RelationList`, extends :attr:`value`, :attr:`relations` and :attr:`elm` with the ones in *other*.

   If *other* is a :class:`list`, extends :attr:`value` with *other*.

.. method:: RelationList.__bool__() -> bool

   Called with :class:`bool()`. Returns :data:`bool(`:attr:`value`:data:`)`.

.. method:: RelationList.__contains__(other) -> bool

   Called with :data:`other in self`. Equal to :data:`other in` :attr:`value`.

.. method:: RelationList.__delitem__(index)

   Called with :data:`del self[x:y:z]`. Calls :meth:`delete` for each element in the range of :attr:`value`.

.. method:: RelationList.__eq__(other) -> bool

   Called with :data:`self == other`. If *other* is a :class:`RelationList`, returns :class:`True` if :attr:`value` and :attr:`relations` are equal, else :class:`False`.

.. method:: RelationList.__format__(fmt='%L') -> str

   Called with :data:`format(self, fmt)`.

   Format table:

   +-------------+------------------------------+
   | Format Code |           Definition         |
   +=============+==============================+
   |  :data:`%L` |     Inserts :attr:`value`.   |
   +-------------+------------------------------+
   |  :data:`%R` |  Inserts :attr:`relations`.  |
   +-------------+------------------------------+
   |  :data:`%E` |      Inserts :attr:`elm`.    |
   +-------------+------------------------------+
   |  :data:`%T` | Inserts :data:`tuple(value)`.|
   +-------------+------------------------------+

   .. deprecated-removed:: 1.1.0 3.0.0
      The unflexible :data:`%T` format code is deprecated and warns a :class:`PendingDeprecationWarning`. It will be upgraded to :class:`DeprecationWarning` in v2.0         and be removed in v3.0.

.. method:: RelationList.__getitem__(index)

   Called with :data:`self[index]`. Returns :attr:`value`:data:`[index]`.

.. method:: RelationList.__iter__()

   Called with :meth:`iter`, and converted to different types by :class:`list()`, :class:`tuple()`, :class:`dict()` and :class:`set()`. Returns :data:`iter(`:attr:`value`:data:`)`.

   .. versionchanged:: 1.1.0
      :data:`iter(value)` is returned instead of :data:`iter(elm)`. Programs that need to support older versions should simply switch to :data:`iter(elm)`.

.. method:: RelationList.__len__() -> int

   Called with :meth:`len`. Returns :data:`len(`:attr:`value`:data:`)`.

.. method:: RelationList.__or__(other)

   This is *not* called by :data:`self or other` (That's done by :meth:`__bool__`). It's called by :data:`self | other`.

   If *other* is a :class:`RelationList`, returns a new :class:`RelationList` with :attr:`value` equaling the two :attr:`values` added, having no relations.

   If *other* is a :class:`list`, returns a new :class:`RelationList` with :attr:`value` equaling :attr:`value` plus *other*.

.. method:: RelationList.__ror__(other)

   This is *not* called by :data:`other or self` (That's done by :meth:`other.__bool__`). It's called by :data:`other | self`. Same as :attr:`__or__`, but *other* is inserted *before* :attr:`value`.

.. method:: RelationList.__repr__() -> str

   Called by :meth:`repr`. Returns :data:`RelationList(value)`, with :data:`[]` removed.

   .. versionchanged:: 1.1.0
      The :data:`RelationList` prefix is added, and :attr:`relations` and :attr:`elm` are no longer added. This is an incompatible change.

.. method:: RelationList.__reversed__()

   Called by :meth:`reversed`. Returns a new :class:`RelationList` with :attr:`value` reversed. Relations are not preserved.

.. method:: RelationList.__setitem__(key, value)

   Called by :data:`self.[x:y:z] = [...]`. Same as :attr:`value`:data:`[x:y:z] = [...]`. All relations related to the replaced values will be processed by :meth:`delete`.

.. method:: RelationList.__str__() -> str

   Called by :meth:`str`. Returns :data:`str(`:attr:`value`:data:`)`.

Context Manager
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

:class:`RelationList` has :meth:`__enter__` and :meth:`__exit__` methods, so it can be used as a context manager. All relations are cleared after the block is exited, and then exceptions will be re-raised if raised.

Example:

.. code:: python

   >>> import relationlist
   >>> with relationlist.RelationList([1, 2, 3]) as x:
   ...     x.relate(1, 2, 'break', 3)
   ...     x.relate(1, 3, 'delete', 4)
   ...     x.relate(1, 4, 'break', 5)
   ...     print(x.relations)
   ...     raise ValueError
   ...
   [(1, 2, 'break', 3), (1, 3, 'delete', 4), (2, 3, 'break', 5)]
   Traceback (most recent call last):
     File "<pyshell#2>", line 6, in <module>
       raise ValueError
   ValueError
   >>> x.relations
   []

|

`Changelog → <./changelog.html>`_
