SplashData
==========

is created from.

Inherit:
	:doc:`GameBaseData`

Description
-----------

Acts as the physical point in space in white a Splash is created from.


Fields
------


.. cpp:member:: float  SplashData::acceleration

	Constant acceleration value to place upon the splash effect.

.. cpp:member:: ColorF  SplashData::colors [4]

	Color values to set the splash effect, rgba. Up to 4 allowed. Will transition through colors based on values set in the times value. Example: colors[0] = "0.6 1.0 1.0 0.5".

.. cpp:member:: int  SplashData::delayMS

	Time to delay, in milliseconds, before actually starting this effect.

.. cpp:member:: int  SplashData::delayVariance

	Time variance for delayMS.

.. cpp:member:: float  SplashData::ejectionAngle

	Rotational angle to create a splash ring.

.. cpp:member:: float  SplashData::ejectionFreq

	Frequency in which to emit splash rings.

.. cpp:member:: ParticleEmitterData SplashData::emitter [3]

	List of particle emitters to create at the point of this Splash effect.

.. cpp:member:: ExplosionData SplashData::Explosion

	ExplosionData object to create at the creation position of this splash effect.

.. cpp:member:: float  SplashData::height

	Height for the splash to reach.

.. cpp:member:: int  SplashData::lifetimeMS

	Lifetime for this effect, in milliseconds.

.. cpp:member:: int  SplashData::lifetimeVariance

	Time variance for lifetimeMS.

.. cpp:member:: int  SplashData::numSegments

	Number of ejection points in the splash ring.

.. cpp:member:: float  SplashData::ringLifetime

	Lifetime, in milliseconds, for a splash ring.

.. cpp:member:: Point3F  SplashData::scale

	The scale of this splashing effect, defined as the F32 points X, Y, Z.

.. cpp:member:: SFXProfile SplashData::soundProfile

	SFXProfile effect to play.

.. cpp:member:: float  SplashData::startRadius

	Starting radius size of a splash ring.

.. cpp:member:: float  SplashData::texFactor

	Factor in which to apply the texture to the splash ring, 0.0f - 1.0f.

.. cpp:member:: filename  SplashData::texture [2]

	Imagemap file to use as the texture for the splash effect.

.. cpp:member:: float  SplashData::texWrap

	Amount to wrap the texture around the splash ring, 0.0f - 1.0f.

.. cpp:member:: float  SplashData::times [4]

	Times to transition through the splash effect. Up to 4 allowed. Values are 0.0 - 1.0, and corrispond to the life of the particle where 0 is first created and 1 is end of lifespace.

.. cpp:member:: float  SplashData::velocity

	Velocity for the splash effect to travel.

.. cpp:member:: float  SplashData::width

	Width for the X and Y coordinates to create this effect within.
