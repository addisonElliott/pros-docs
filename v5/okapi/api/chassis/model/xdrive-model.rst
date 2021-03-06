=============
X-Drive Model
=============

.. contents:: :local:


okapi::XDriveModelArgs
======================

Data class for the arguments to ``XDriveModel``.

Constructor(s)
--------------

This constructor infers the encoders from the top left and top right motors.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        XDriveModelArgs(std::shared_ptr<AbstractMotor> itopLeftMotor,
                        std::shared_ptr<AbstractMotor> itopRightMotor,
                        std::shared_ptr<AbstractMotor> ibottomRightMotor,
                        std::shared_ptr<AbstractMotor> ibottomLeftMotor,
                        double imaxOutput = 127)

==================   ===================================================================
 Parameters
==================   ===================================================================
 itopLeftMotor        The top left motor.
 itopRightMotor       The top right motor.
 ibottomRightMotor    The bottom right motor.
 ibottomLeftMotor     The bottom left motor.
 imaxOutput           The maximum output value to the motors.
==================   ===================================================================

This constructor does not infer the encoders from the motors, and instead takes explicitly specified encoders.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        XDriveModelArgs(std::shared_ptr<AbstractMotor> itopLeftMotor,
                        std::shared_ptr<AbstractMotor> itopRightMotor,
                        std::shared_ptr<AbstractMotor> ibottomRightMotor,
                        std::shared_ptr<AbstractMotor> ibottomLeftMotor,
                        std::shared_ptr<ContinuousRotarySensor> ileftEnc,
                        std::shared_ptr<ContinuousRotarySensor> irightEnc,
                        double imaxOutput = 127)

==================   ===================================================================
 Parameters
==================   ===================================================================
 itopLeftMotor        The top left motor.
 itopRightMotor       The top right motor.
 ibottomRightMotor    The bottom right motor.
 ibottomLeftMotor     The bottom left motor.
 ileftEnc             The left side encoder.
 irightEnc            The right side encoder.
 imaxOutput           The maximum output value to the motors.
==================   ===================================================================

----

okapi::XDriveModel
==================

The model for an x-drive chassis. If you are trying to make an instance of this class, you should
most likely be creating a type of
`ChassisController <../controller/abstract-chassis-controller.html>`_ instead. If you really do
mean to make an instance of a
`ChassisModel <abstract-chassis-model.html>`_, then you should probably be using the
`ChassisModelFactory <chassis-model-factory.html>`_ instead of a constructor from this class.

Constructor(s)
--------------

This constructor infers the encoders from the motors.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        XDriveModel(std::shared_ptr<AbstractMotor> itopLeftMotor,
                    std::shared_ptr<AbstractMotor> itopRightMotor,
                    std::shared_ptr<AbstractMotor> ibottomRightMotor,
                    std::shared_ptr<AbstractMotor> ibottomLeftMotor,
                    double imaxOutput = 127)

==================   ===================================================================
 Parameters
==================   ===================================================================
 itopLeftMotor        The top left motor.
 itopRightMotor       The top right motor.
 ibottomRightMotor    The bottom right motor.
 ibottomLeftMotor     The bottom left motor.
 imaxOutput           The maximum output value to the motors.
==================   ===================================================================

This constructor does not infer the encoders from the motors, and instead takes explicitly specified encoders.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        XDriveModel(std::shared_ptr<AbstractMotor> itopLeftMotor,
                    std::shared_ptr<AbstractMotor> itopRightMotor,
                    std::shared_ptr<AbstractMotor> ibottomRightMotor,
                    std::shared_ptr<AbstractMotor> ibottomLeftMotor,
                    std::shared_ptr<ContinuousRotarySensor> ileftEnc,
                    std::shared_ptr<ContinuousRotarySensor> irightEnc,
                    double imaxOutput = 127)

==================   ===================================================================
 Parameters
==================   ===================================================================
 itopLeftMotor        The top left motor.
 itopRightMotor       The top right motor.
 ibottomRightMotor    The bottom right motor.
 ibottomLeftMotor     The bottom left motor.
 ileftEnc             The left side encoder.
 irightEnc            The right side encoder.
 imaxOutput           The maximum output value to the motors.
==================   ===================================================================

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        explicit XDriveModel(const XDriveModelArgs &iparams)

==================   ===================================================================
 Parameters
==================   ===================================================================
 iparams              The ``XDriveModel`` arguments.
==================   ===================================================================

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        XDriveModel(const XDriveModel &other)

==================   ===================================================================
 Parameters
==================   ===================================================================
 other                Copy constructor.
==================   ===================================================================

Methods
-------

forward
~~~~~~~

Drives the robot forwards (using open-loop control).

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void forward(double ispeed) const override

=============== ===================================================================
Parameters
=============== ===================================================================
 ispeed          The motor power.
=============== ===================================================================

----

driveVector
~~~~~~~~~~~

Drives the robot in an arc (using open-loop control).

The algorithm is (approximately):
::

  leftPower = ySpeed + zRotation
  rightPower = ySpeed - zRotation

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void driveVector(double iySpeed, double izRotation) const override

=============== ===================================================================
Parameters
=============== ===================================================================
 iySpeed         The speed on the y axis (forward).
 izRotation      The speed around the z axis (up).
=============== ===================================================================

----

rotate
~~~~~~

Turns the robot clockwise (using open-loop control).

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void rotate(double ispeed) const override

=============== ===================================================================
Parameters
=============== ===================================================================
 ispeed          The motor power.
=============== ===================================================================

----

stop
~~~~

Stops the robot (set all the motors to ``0``).

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void stop() const override

----

tank
~~~~

Drives the robot with a tank drive layout. Uses voltage mode.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void tank(double ileftSpeed, double irightSpeed, double ithreshold = 0) const override

=============== ===================================================================
Parameters
=============== ===================================================================
 ileftSpeed      The left side speed.
 irightSpeed     The right side speed.
 ithreshold      The joystick deadband.
=============== ===================================================================

----

arcade
~~~~~~

Drives the robot with an arcade drive layout. Uses voltage mode.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void arcade(double iySpeed, double izRotation, double ithreshold = 0) const override

=============== ===================================================================
Parameters
=============== ===================================================================
 iySpeed         The speed on the y axis (forward).
 izRotation      The speed around the z axis (up).
 ithreshold      The joystick deadband.
=============== ===================================================================

----

xArcade
~~~~~~~

Drives the robot with an arcade drive layout. Uses voltage mode.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        virtual void xArcade(double ixSpeed, double iySpeed, double izRotation, double ithreshold = 0) const

=============== ===================================================================
Parameters
=============== ===================================================================
 ixSpeed         The speed on the x axis (right).
 iySpeed         The speed on the y axis (forward).
 izRotation      The speed around the z axis (up).
 ithreshold      The joystick deadband.
=============== ===================================================================

----

left
~~~~

Powers the left side motors.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void left(double ispeed) const override

=============== ===================================================================
Parameters
=============== ===================================================================
 ispeed          The new speed.
=============== ===================================================================

----

right
~~~~~

Powers the right side motors.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void right(double ispeed) const override

=============== ===================================================================
Parameters
=============== ===================================================================
 ispeed          The new speed.
=============== ===================================================================

----

getSensorVals
~~~~~~~~~~~~~

Returns the current sensor values. Ideally, return the values in the format ``{left, right, ...}``.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        std::valarray<std::int32_t> getSensorVals() const override

**Returns:** The current sensor values (the formatting is implementation dependent).

----

resetSensors
~~~~~~~~~~~~

Resets the sensors to their zero point.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void resetSensors() const override

----

setBrakeMode
~~~~~~~~~~~~

Sets the brake mode for each motor.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void setBrakeMode(AbstractMotor::brakeMode mode) const override

=============== ===================================================================
Parameters
=============== ===================================================================
 mode            The new brake mode.
=============== ===================================================================

----

setEncoderUnits
~~~~~~~~~~~~~~~

Sets the encoder units for each motor.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void setEncoderUnits(AbstractMotor::encoderUnits units) const override

=============== ===================================================================
Parameters
=============== ===================================================================
 units           The new units.
=============== ===================================================================

----

setGearing
~~~~~~~~~~

Sets the gearset for each motor.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        void setGearing(AbstractMotor::gearset gearset) const override

=============== ===================================================================
Parameters
=============== ===================================================================
 gearset         The new gearset.
=============== ===================================================================

----

getTopLeftMotor
~~~~~~~~~~~~~~~

Returns the top left motor.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        std::shared_ptr<AbstractMotor> getTopLeftMotor() const

**Returns:** The top left motor.

----

getTopRightMotor
~~~~~~~~~~~~~~~~

Returns the top right motor.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        std::shared_ptr<AbstractMotor> getTopRightMotor() const

**Returns:** The top right motor.

----

getBottomRightMotor
~~~~~~~~~~~~~~~~~~~

Returns the bottom right motor.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        std::shared_ptr<AbstractMotor> getBottomRightMotor() const

**Returns:** The bottom right motor.

----

getBottomLeftMotor
~~~~~~~~~~~~~~~~~~

Returns the bottom left motor.

.. tabs ::
   .. tab :: Prototype
      .. highlight:: cpp
      ::

        std::shared_ptr<AbstractMotor> getBottomLeftMotor() const

**Returns:** The bottom left motor.
