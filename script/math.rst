Math
====

Functions for dealing with vectors and matrices etc.

Functions
---------

.. cpp:function:: Point3F getBoxCenter(Box3F box)

	Get the center point of an axis-aligned box.

	:param b: A Box3F, in string format using "minExtentX minExtentY minExtentZ maxExtentX maxExtentY maxExtentZ"

	:return: Center of the box. 

.. cpp:function:: float getMax(float v1, float v2)

	Calculate the greater of two specified numbers.

	:param v1: Input value.
	:param v2: Input value.

	:return: The greater value of the two specified values. 

.. cpp:function:: float getMin(float v1, float v2)

	Calculate the lesser of two specified numbers.

	:param v1: Input value.
	:param v2: Input value.

	:return: The lesser value of the two specified values. 

.. cpp:function:: float m2Pi()

	Return the value of 2*PI (full-circle in radians).

	:return: The value of 2*PI. 

.. cpp:function:: float mAbs(float v)

	Calculate absolute value of specified value.

	:param v: Input Value.

	:return: Absolute value of specified value. 

.. cpp:function:: float mAcos(float v)

	Calculate the arc-cosine of v.

	:param v: Input Value (in radians).

	:return: The arc-cosine of the input value. 

.. cpp:function:: float mAsin(float v)

	Calculate the arc-sine of v.

	:param v: Input Value (in radians).

	:return: The arc-sine of the input value. 

.. cpp:function:: float mAtan(float rise, float run)

	Calculate the arc-tangent (slope) of a line defined by rise and run.

	:param rise: of line.
	:param run: of line.

	:return: The arc-tangent (slope) of a line defined by rise and run. 

.. cpp:function:: void mathInit( ...)

	Install the math library with specified extensions. Possible parameters are: 
	
	* 'DETECT' Autodetect math lib settings.
	* 'C' Enable the C math routines. C routines are always enabled.
	* 'FPU' Enable floating point unit routines.
	* 'MMX' Enable MMX math routines.
	* '3DNOW' Enable 3dNow! math routines.
	* 'SSE' Enable SSE math routines. 

.. cpp:function:: int mCeil(float v)

	Round v up to the nearest integer.

	:param v: Number to convert to integer.

	:return: Number converted to integer. 

.. cpp:function:: float mClamp(float v, float min, float max)

	Clamp the specified value between two bounds.

	:param v: Input value.
	:param min: Minimum Bound.
	:param max: Maximum Bound.

	:return: The specified value clamped to the specified bounds. 

.. cpp:function:: float mCos(float v)

	Calculate the cosine of v.

	:param v: Input Value (in radians).

	:return: The cosine of the input value. 

.. cpp:function:: float mDegToRad(float degrees)

	Convert specified degrees into radians.

	:param degrees: Input Value (in degrees).

	:return: The specified degrees value converted to radians. 

.. cpp:function:: string mFloatLength(float v, int precision)

	Formats the specified number to the given number of decimal places.

	:param v: Number to format.
	:param precision: Number of decimal places to format to (1-9).

	:return: Number formatted to the specified number of decimal places. 

.. cpp:function:: int mFloor(float v)

	Round v down to the nearest integer.

	:param v: Number to convert to integer.

	:return: Number converted to integer. 

.. cpp:function:: float mFMod(float v, float d)

	Calculate the remainder of v/d.

	:param v: Input Value.
	:param d: Divisor Value.

	:return: The remainder of v/d. 

.. cpp:function:: bool mIsPow2(int v)

	Returns whether the value is an exact power of two.

	:param v: Input value.

	:return: Whether the specified value is an exact power of two. 

.. cpp:function:: float mLerp(float v1, float v2, float time)

	Calculate linearly interpolated value between two specified numbers using specified normalized time.

	:param v1: Interpolate From Input value.
	:param v2: Interpolate To Input value.
	:param time: Normalized time used to interpolate values (0-1).

	:return: The interpolated value between the two specified values at normalized time t. 

.. cpp:function:: float mLog(float v)

	Calculate the natural logarithm of v.

	:param v: Input Value.

	:return: The natural logarithm of the input value. 

.. cpp:function:: float mPi()

	Return the value of PI (half-circle in radians).

	:return: The value of PI. 

.. cpp:function:: float mPow(float v, float p)

	Calculate b raised to the p-th power.

	:param v: Input Value.
	:param p: Power to raise value by.

	:return: v raised to the p-th power. 

.. cpp:function:: float mRadToDeg(float radians)

	Convert specified radians into degrees.

	:param radians: Input Value (in radians).

	:return: The specified radians value converted to degrees. 

.. cpp:function:: int mRound(float v)

	Round v to the nearest integer.

	:param v: Number to convert to integer.

	:return: Number converted to integer. 

.. cpp:function:: float mSaturate(float v)

	Clamp the specified value between 0 and 1 (inclusive).

	:param v: Input value.

	:return: The specified value clamped between 0 and 1 (inclusive). 

.. cpp:function:: float mSin(float v)

	Calculate the sine of v.

	:param v: Input Value (in radians).

	:return: The sine of the input value. 

.. cpp:function:: string mSolveCubic(float a, float b, float c, float d)

	Solve a cubic equation (3rd degree polynomial) of form a*x^3 + b*x^2 + c*x + d = 0.

	:param a: First Coefficient.
	:param b: Second Coefficient.
	:param c: Third Coefficient.
	:param d: Fourth Coefficient.

	:return: A 4-tuple, containing: (sol x0 x1 x2). (sol) is the number of solutions(being 0, 1, 2 or 3), and (x0), (x1) and (x2) are the solutions, if any. 

.. cpp:function:: string mSolveQuadratic(float a, float b, float c)

	Solve a quadratic equation (2nd degree polynomial) of form a*x^2 + b*x + c = 0.

	:param a: First Coefficient.
	:param b: Second Coefficient.
	:param c: Third Coefficient.

	:return: A triple, containing: (sol x0 x1). (sol) is the number of solutions(being 0, 1, or 2), and (x0) and (x1) are the solutions, if any. 

.. cpp:function:: string mSolveQuartic(float a, float b, float c, float d, float e)

	Solve a quartic equation (4th degree polynomial) of form a*x^4 + b*x^3 + c*x^2 + d*x + e = 0.

	:param a: First Coefficient.
	:param b: Second Coefficient.
	:param c: Third Coefficient.
	:param d: Fourth Coefficient.
	:param e: Fifth Coefficient.

	:return: A 5-tuple, containing: (sol x0 x1 x2 c3). (sol) is the number of solutions(being 0, 1, 2, 3 or 4), and (x0), (x1), (x2) and (x3) are the solutions, if any. 

.. cpp:function:: float mSqrt(float v)

	Calculate the square-root of v.

	:param v: Input Value.

	:return: The square-root of the input value. 

.. cpp:function:: float mTan(float v)

	Calculate the tangent of v.

	:param v: Input Value (in radians).

	:return: The tangent of the input value. 

Vector Math
------------

Functions for working with three-dimensional vectors (VectorF/Point3F).

Functions
~~~~~~~~~

.. cpp:function:: VectorF VectorAdd(VectorF a, VectorF b)

	Add two vectors.

	:param a: The first vector.
	:param b: The second vector.

	:return: .

	Example::


		// VectorAdd( %a, %b );
		// The sum of vector a, (ax, ay, az), and vector b, (bx, by, bz) is:
		//     a + b = ( ax + bx, ay + by, az + bz )

		%a = "1 0 0";
		%b = "0 1 0";
		
		// %r = "( 1 + 0, 0 + 1, 0 + 0 )";// %r = "1 1 0";
		%r = VectorAdd( %a, %b );

.. cpp:function:: VectorF VectorCross(VectorF a, VectorF b)

	Calculcate the cross product of two vectors.

	:param a: The first vector.
	:param b: The second vector.

	:return: .

	Example::

		// VectorCross( %a, %b );
		// The cross product of vector a, (ax, ay, az), and vector b, (bx, by, bz), is
		//     a x b = ( ( ay * bz ) - ( az * by ), ( az * bx ) - ( ax * bz ), ( ax * by ) - ( ay * bx ) )
		
		%a = "1 1 0";
		%b = "2 0 1";
		
		// %r = "( ( 1 * 1 ) - ( 0 * 0 ), ( 0 * 2 ) - ( 1 * 1 ), ( 1 * 0 ) - ( 1 * 2 ) )";
		// %r = "1 -1 -2";
		%r = VectorCross( %a, %b );

.. cpp:function:: float VectorDist(VectorF a, VectorF b)

	Compute the distance between two vectors.

	:param a: The first vector.
	:param b: The second vector.

	:return:  ).

	Example::

		// VectorDist( %a, %b );
		// The distance between vector a, (ax, ay, az), and vector b, (bx, by, bz), is
		//     a -> b = ||( b - a )||
		//            = ||( bx - ax, by - ay, bz - az )||
		//            = mSqrt( ( bx - ax ) * ( bx - ax ) + ( by - ay ) * ( by - ay ) + ( bz - az ) * ( bz - az ) )
		
		%a = "1 1 0";
		%b = "2 0 1";
		
		// %r = mSqrt( ( 2 - 1 ) * ( 2 - 1) + ( 0 - 1 ) * ( 0 - 1 ) + ( 1 - 0 ) * ( 1 - 0 ) );
		// %r = mSqrt( 3 );
		%r = VectorDist( %a, %b );

.. cpp:function:: float VectorDot(VectorF a, VectorF b)

	Compute the dot product of two vectors.

	:param a: The first vector.
	:param b: The second vector.

	:return: .

	Example::

		// VectorDot( %a, %b );
		// The dot product between vector a, (ax, ay, az), and vector b, (bx, by, bz), is:
		//     a . b = ( ax * bx + ay * by + az * bz )
		
		%a = "1 1 0";
		%b = "2 0 1";
		
		// %r = "( 1 * 2 + 1 * 0 + 0 * 1 )";
		// %r = 2;
		%r = VectorDot( %a, %b );

.. cpp:function:: float VectorLen(VectorF v)

	Calculate the magnitude of the given vector.

	:param v: A vector.

	:return: .

	Example::

		// VectorLen( %a );
		// The length or magnitude of  vector a, (ax, ay, az), is:
		//     ||a|| = Sqrt( ax * ax + ay * ay + az * az )
		
		%a = "1 1 0";
		
		// %r = mSqrt( 1 * 1 + 1 * 1 + 0 * 0 );
		// %r = mSqrt( 2 );
		// %r = 1.414;
		%r = VectorLen( %a );

.. cpp:function:: VectorF VectorLerp(VectorF a, VectorF b, float t)

	Linearly interpolate between two vectors by t .

	:param a: Vector to start interpolation from.
	:param b: Vector to interpolate to.
	:param t: Interpolation factor (0-1). At zero, a is returned and at one, b is returned. In between, an interpolated vector between a and b is returned.

	:return: .

	Example::

		// VectorLerp( %a, %b );
		// The point between vector a, (ax, ay, az), and vector b, (bx, by, bz), which is
		// weighted by the interpolation factor, t, is
		//     r = a + t * ( b - a )
		//       = ( ax + t * ( bx - ax ), ay + t * ( by - ay ), az + t * ( bz - az ) )
		
		%a = "1 1 0";
		%b = "2 0 1";
		%v = "0.25";
		
		// %r = "( 1 + 0.25 * ( 2 - 1 ), 1 + 0.25 * ( 0 - 1 ), 0 + 0.25 * ( 1 - 0 ) )";
		// %r = "1.25 0.75 0.25";
		%r = VectorLerp( %a, %b );

.. cpp:function:: VectorF VectorNormalize(VectorF v)

	Brings a vector into its unit form, i.e. such that it has the magnitute 1.

	:param v: The vector to normalize.

	:return:  scaled to length 1.

	Example::

		// VectorNormalize( %a );
		// The normalized vector a, (ax, ay, az), is:
		//     a^ = a / ||a||
		//        = ( ax / ||a||, ay / ||a||, az / ||a|| )
		
		%a = "1 1 0";
		%l = 1.414;
		
		// %r = "( 1 / 1.141, 1 / 1.141, 0 / 1.141 )";
		// %r = "0.707 0.707 0";
		%r = VectorNormalize( %a );

.. cpp:function:: MatrixF VectorOrthoBasis(AngAxisF aa)

	Create an orthogonal basis from the given vector.

	:param aaf: The vector to create the orthogonal basis from.

	:return: A matrix representing the orthogonal basis. 

.. cpp:function:: VectorF VectorScale(VectorF a, float scalar)

	Scales a vector by a scalar.

	:param a: The vector to scale.
	:param scalar: The scale factor.

	:return: .

	Example::

		// VectorScale( %a, %v );
		// Scaling vector a, (ax, ay, az), but the scalar, v, is:
		//     a * v = ( ax * v, ay * v, az * v )
		
		%a = "1 1 0";
		%v = "2";
		
		// %r = "( 1 * 2, 1 * 2, 0 * 2 )";
		// %r = "2 2 0";
		%r = VectorScale( %a, %v );

.. cpp:function:: VectorF VectorSub(VectorF a, VectorF b)

	Subtract two vectors.

	:param a: The first vector.
	:param b: The second vector.

	:return: .

	Example::

		// VectorSub( %a, %b );
		// The difference of vector a, (ax, ay, az), and vector b, (bx, by, bz) is:
		//     a - b = ( ax - bx, ay - by, az - bz )
		
		%a = "1 0 0";
		%b = "0 1 0";
		
		// %r = "( 1 - 0, 0 - 1, 0 - 0 )";
		// %r = "1 -1 0";
		%r = VectorSub( %a, %b );

Matrix Math
-----------

Functions for working with matrices (MatrixF, AngAxisF, MatrixRotation, MatrixPosition).


Functions
~~~~~~~~~

.. cpp:function:: TransformF MatrixCreate(VectorF position, AngAxisF orientation)

	Create a transform from the given translation and orientation.

	:param position: The translation vector for the transform.
	:param orientation: The axis and rotation that orients the transform.

	:return: A transform based on the given position and orientation. 

.. cpp:function:: TransformF MatrixCreateFromEuler(Point3F angles)

	a matrix from the given rotations.

	:param Vector3F: X, Y, and Z rotation in *radians*.

	:return: A transform based on the given orientation. 

.. cpp:function:: Point3F MatrixMulPoint(TransformF transform, Point3F point)

	Multiply the given point by the given transform assuming that w=1. This function will multiply the given vector such that translation with take effect.

	:param transform: A transform.
	:param point: A vector.

	:return: The transformed vector. 

.. cpp:function:: TransformF MatrixMultiply(TransformF left, TransformF right)

	Multiply the two matrices.

	:param left: First transform.
	:param right: Right transform.

	:return: Concatenation of the two transforms. 

.. cpp:function:: VectorF MatrixMulVector(TransformF transform, VectorF vector)

	Multiply the vector by the transform assuming that w=0. This function will multiply the given vector by the given transform such that translation will not affect the vector.

	:param transform: A transform.
	:param vector: A vector.

	:return: The transformed vector. 

Random Numbers
--------------

Functions for generating random numbers. Based on a seed, the random number generator produces a sequence of numbers. As a given seed will always produce the same sequence of numbers this can be used to generate re-producible sequences of apparently random numbers. To set the seed, call setRandomSeed().

Functions
~~~~~~~~~

.. cpp:function:: float getRandom(int a, int b)

	Returns a random number based on parameters passed in.. If no parameters are passed in, getRandom() will return a float between 0.0 and 1.0. If one parameter is passed an integer between 0 and the passed in value will be returned. Two parameters will return an integer between the specified numbers.

	:param a: If this is the only parameter, a number between 0 and a is returned. Elsewise represents the lower bound.
	:param b: Upper bound on the random number. The random number will be <= b.

	:return: , between 0 and a, or a float between 0.0 and 1.1 depending on usage.

.. cpp:function:: int getRandomSeed()

	Get the current seed used by the random number generator.

	:return: The current random number generator seed value. 

.. cpp:function:: void setRandomSeed(int seed)

	Set the current seed for the random number generator. Based on this seed, a repeatable sequence of numbers will be produced by getRandom() .

	:param seed: The seed with which to initialize the randon number generator with. The same seed will always leed tothe same sequence of pseudo-random numbers. If -1, the current timestamp will be used as the seed which is a good basis for randomization.
