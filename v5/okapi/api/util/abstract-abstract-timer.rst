=========================
(Abstract) Abstract Timer
=========================

.. contents:: :local:

okapi::AbstractTimer
====================

A time- and timing-related utility class.

Methods
-------

millis
~~~~~~

Returns the current time in units of ``QTime``.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual QTime millis() const = 0

**Returns:** The current time in units of ``QTime``.

getDt
~~~~~

Returns the time passed in ms since the previous call of this function.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual QTime getDt() = 0

**Returns:** The time passed in ms since the previous call of this function.

----

getStartingTime
~~~~~~~~~~~~~~~

Returns the time the timer was first constructed.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual QTime getStartingTime() const = 0

**Returns:** The time the timer was first constructed.

----

getDtFromStart
~~~~~~~~~~~~~~

Returns the time since the timer was first constructed.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual QTime getDtFromStart() const = 0

**Returns:** The time since the timer was first constructed.

----

placeMark
~~~~~~~~~

Place a time marker. Placing another marker will overwrite the previous one.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual void placeMark() = 0

----

placeHardMark
~~~~~~~~~~~~~

Place a hard time marker. Placing another hard marker will not overwrite the previous one; instead, call ``clearHardMark()`` and then place another.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual void placeHardMark() = 0

----

clearHardMark
~~~~~~~~~~~~~

Clears the hard marker.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual QTime clearHardMark() = 0

**Returns:** The old hard marker.

----

getDtFromMark
~~~~~~~~~~~~~

Returns the time since the time marker.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual QTime getDtFromMark() const = 0

**Returns:** The time since the time marker.

----

getDtFromHardMark
~~~~~~~~~~~~~~~~~

Returns the time since the hard time marker.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual QTime getDtFromHardMark() const = 0

**Returns:** The time since the hard time marker.

----

repeat
~~~~~~

Returns ``true`` when the input time period has passed, then resets. Meant to be used in loops to
run an action every time period without blocking.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual bool repeat(QTime time) = 0

   .. tab :: Example
      .. highlight:: cpp
      ::

        void opcontrol() {
          okapi::Timer timer;
          while (true) {
            if (timer.repeat(100_ms)) {
              // Do something every 100 ms
            }
            pros::delay(10);
          }
        }

============ ===============================================================
 Parameters
============ ===============================================================
 time           The time period.
============ ===============================================================

**Returns:** ``true`` when the input time period has passed, ``false`` after reading ``true`` until
the period has passed again

----

repeat
~~~~~~

Returns ``true`` when the input time period has passed, then resets. Meant to be used in loops to
run an action every time period without blocking.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual bool repeat(QFrequency time) = 0

   .. tab :: Example
      .. highlight:: cpp
      ::

        void opcontrol() {
          okapi::Timer timer;
          while (true) {
            if (timer.repeat(10_Hz)) {
              // Do something 10 times per second
            }
            pros::delay(10);
          }
        }

============ ===============================================================
 Parameters
============ ===============================================================
 frequency    The repeat frequency.
============ ===============================================================

**Returns:** ``true`` when the input time period has passed, ``false`` after reading ``true`` until
the period has passed again
