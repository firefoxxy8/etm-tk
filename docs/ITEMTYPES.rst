Item types
==========

There are several types of items in etm. Each item begins with a type
character such as an asterisk (event) and continues on one or more lines
either until the end of the file is reached or another line is found
that begins with a type character. The type character for each item is
followed by the item summary and then, perhaps, by one or more
``@key value`` pairs - see :ref:`@Keys <keys-label>` for details. The order in
which such pairs are entered does not matter.

~ Action
--------

A record of the expenditure of time (``@e``) and/or money (``@x``).
Actions are not reminders, they are instead records of how time and/or
money was actually spent. Action lines begin with a tilde, ``~``.

::

        ~ picked up lumber and paint @s mon 3p @e 1h15m @x 127.32

Entries such as ``@s mon 3p``, ``@e 1h15m`` and ``@x 127.32`` are
discussed below under *Item details*. Action entries form the basis for
time and expense billing using action type custom views - see :ref:`Custom
view <custom-label>` for details.

Tip: You can use either path or keyword or a combination of the two to
organize your actions.

\* Event
--------

Something that will happen on particular day(s) and time(s). Event lines
begin with an asterick, ``*``.

::

        * dinner with Karen and Al @s sat 7p @e 3h

Events have a starting datetime, ``@s`` and an extent, ``@e``. The
ending datetime is given implicitly as the sum of the starting datetime
and the extent. Events that span more than one day are possible, e.g.,

::

        * Sales conference @s 9a wed @e 2d8h

begins at 9am on Wednesday and ends at 5pm on Friday.

An event without an ``@e`` entry or with ``@e 0`` is regarded as a
*reminder* and, since there is no extent, will not be displayed in *busy
times*.

^ Occasion
----------

Holidays, anniversaries, birthdays and such. Similar to an event with a
date but no starting time and no extent. Occasions begin with a caret
sign, ``^``.

::

        ^ The !1776! Independence Day @s 2010-07-04 @r y &M 7 &m 4

On July 4, 2013, this would appear as ``The 237th Independence Day``.
Here !1776! is an example of an *anniversary substitution* - see
:ref:`Dates <dates-label>` for details.

! Note
------

A record of some useful information. Note lines begin with an
exclamation point, ``!``.

::

    ! xyz software @k software:passwords @d user: dnlg, pw: abc123def

Tip: Since both the GUI and CLI note views group and sort by keyword, it
is a good idea to use keywords to organize your notes.

-, % and + Tasks
----------------

Tasks are reminders of something that needs to be done. There are three
possible type characters for tasks: ``-``, ``%`` and ``+``; these are
discussed below. Each of these can be further distinguished by whether
or not the task has entries for ``@e`` and/or ``@s``.

When an ``@e`` (extent) is provided for any type of task, it is regarded
as an estimate of the time required to complete the task.

-  Tasks without an ``@s`` entry have no due date and are to be done
   whenever convenient.

-  Tasks with an ``@s`` entry that specifies ``12am`` (or ``0h``) as the
   starting time are to be completed on or before the date specified.

-  Tasks with an ``@s`` entry that specifies a starting time *other
   than* ``12am`` (or ``0h``) but without an ``@e`` entry are to be
   completed on or before the date *and time* specified. These will be
   displayed in etm Agenda and Day views before other tasks, sorted by
   and displaying the starting time.

-  Tasks with an ``@s`` entry that specifies a starting time *other
   than* ``12am`` (or ``0h``) and with an ``@e`` entry are to be
   completed during the period that extends from the starting time until
   ``@e`` after the starting time. These will be displayed in etm Agenda
   and Day views before other tasks, sorted by and displaying the time
   period in the same manner as events. This period will be regarded as
   busy time and treated as such by etm in, e.g., Week view. [Tip: Use a
   non-midnight starting time and an extent when you want to block off a
   specific period to complete a task.]

\- Task
~~~~~~~

This is the basic task and begins with a minus sign, ``-``.

::

    - pay bills @s Oct 25

A task with an ``@s`` entry becomes due on that date and time and past
due when that date has passed. If the task also has an ``@b`` begin-by
entry, then advance warnings of the task will begin appearing the
specified number of days before the task is due.

% Delegated task
~~~~~~~~~~~~~~~~

A task that is assigned to someone else, usually the person designated
in an ``@u`` entry. Delegated tasks begin with a percent sign, ``%``.

::

        % make reservations for trip @u joe @s fri

\+ Task group
~~~~~~~~~~~~~

A collection of related tasks, some of which may be prerequisite for
others. Task groups begin with a plus sign, ``+``.

::

        + dog house
          @j pickup lumber and paint      &q 1
          @j cut pieces                   &q 2
          @j assemble                     &q 3
          @j paint                        &q 4

Note that a task group is a single item and is treated as such. E.g., if
any job is selected for editing then the entire group is displayed.

Individual jobs are given by the ``@j`` entries. The *queue* entries,
``&q``, set the order --- tasks with smaller &q values are prerequisites
for subsequent tasks with larger &q values. In the example above "pickup
lumber and paint" does not have any prerequisites. "Pickup lumber and
paint", however, is a prerequisite for "cut pieces" which, in turn, is a
prerequisite for "assemble". "Assemble", "cut pieces" and "pickup lumber
and paint" are all prerequisites for "paint".

$ In basket
-----------

A quick, don't worry about the details item to be edited later when you
have the time. In basket entries begin with a dollar sign, ``$``.

::

        $ joe 919 123-4567

If you create an item using *etm* and forget to provide a type
character, an ``$`` will automatically be inserted.

? Someday maybe
---------------

Something you don't want to forget about altogether but don't want to
appear on your next or scheduled lists. Someday maybe items begin with a
question mark, ``?``. They are displayed under the heading *Someday* in
Agenda view so that you can easily review them whenever you like.

::

        ? lose weight and exercise more

# Comment
---------

Comments begin with a hash mark, ``#``. Such items are ignored by etm
save for appearing in the path view. Stick a hash mark in front of any
item that you don't want to delete but don't want to see in your other
views.

= Defaults
----------

Default entries begin with an equal sign, ``=``. These entries consist
of ``@key value`` pairs which then become the defaults for subsequent
entries in the same file until another ``=`` entry is reached.

Suppose, for example, that a particular file contains items relating to
"project\_a" for "client\_1". Then entering

::

    = @k client_1:project_a

on the first line of the file and

::

    =

on the twentieth line of the file would set the default keyword for
entries between the first and twentieth line in the file.
