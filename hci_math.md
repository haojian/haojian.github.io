Math
===========

## Beatiful math

- [Euler's Formula for Complex Numbers](https://www.mathsisfun.com/algebra/eulers-formula.html)
	* why e^{ix} = cos x + i sin x

- [Why is 0! = 1?](https://www.youtube.com/watch?v=X32dce7_D48&list=LL3uhKGIAciIX0i206XocM5w&index=3&t=0s)

## Math

- [Spherical coordinate system](https://en.wikipedia.org/wiki/Spherical_coordinate_system)
- [Horizontal coordinate system](https://en.wikipedia.org/wiki/Horizontal_coordinate_system)
	- azimuth and elevation
	- Two angles on perpendicular planes are sufficient to define a vector in 3D space. You could calculate the angle of the projection on the third plane (in this example, XY) using the first two angles. 
	```
	x = Math.cos(alpha)*Math.cos(beta);
	z = Math.sin(alpha)*Math.cos(beta);
	y = Math.sin(beta);
	```
- Rotation problems: 
	1. two types of rotation: rotate the vector, rotate the axes.

- [left/right hand coordination](http://www.euclideanspace.com/maths/geometry/space/coordinates/index.htm)

- [Given vector of one axis, how do I find vectors of other two axes?](http://stackoverflow.com/questions/3049509/given-vector-of-one-axis-how-do-i-find-vectors-of-other-two-axes)
	- 
	```
	Given: Two axes in an arbitrary-basis 3D coordinate system
	To do this, find the cross product.
	[a,b,c] x [d,e,f] = [ b*f - c*e, c*d - a*f, a*e - b*d ]
	```

## Satellite 

- [azimuth and elevation (antenna look angle)](http://www.sattvengg.com/2013/10/azimuth-and-elevation-angle-antenna.html)



##MathJax

- [Grammer reference](http://iori.sinaapp.com/17.html)

## Visualization

- [Multiple Column Histogram](http://www.mathworks.com/matlabcentral/fileexchange/35275-matlab-plot-gallery-histogram-plot/content/html/Histogram_Plot.html)



## Human Motion Tracking

- [Human Motion Analysis](http://www.cs.toronto.edu/~urtasun/courses/ETH10/lecture1.pdf)
- [Human Body Representation](http://www.cs.toronto.edu/~urtasun/courses/ETH10/lecture2.pdf)

##3D Coordination

** Overview **

Terms: Rotation Vectors /Rotation Matrixs / Quaternions / EulerAngles / azimuth-pitch-roll



Yaw, Pitch, Roll is the same like Heading, Attitue, Bank. I

- [Online Convert from Euler to Quaternion](http://quat.zachbennett.com/)

```
Bank - Roll – \phi: rotation about the X-axis
Heading - Pitch – \theta: rotation about the Y-axis
Attitude - Yaw – \psi: rotation about the Z-axis

q1, q2, q3, q4 = w, x, y, z

```


- [Quaternion](http://www.euclideanspace.com/maths/algebra/realNormedAlgebra/quaternions/)

- [Conversion between different format](http://mathworld.wolfram.com/EulerAngles.html)
Rotation Vectors 
- [Understanding Euler Angles](https://www.chrobotics.com/library/understanding-euler-angles)
- [Code in Java](http://code.google.com/p/proscene/source/browse/trunk/src/remixlab/proscene/Quaternion.java?r=479)
- [Yaw, pitch, and roll rotations](http://planning.cs.uiuc.edu/node102.html)
- [Convert 3D vector to Quaternion](http://www.euclideanspace.com/maths/algebra/realNormedAlgebra/quaternions/transforms/derivations/vectors/index.htm)
- [Get the quaternion from two vector](http://lolengine.net/blog/2014/02/24/quaternion-from-two-vectors-final)

** References **

- [Sensor Fusion on Android with code](http://www.thousand-thoughts.com/2012/03/android-sensor-fusion-tutorial/)
- [Particle Filter Simulation in Python](https://github.com/mjl/particle_filter_demo)
- [Quaternions and spatial rotation](http://en.wikipedia.org/wiki/Quaternions_and_spatial_rotation)
- [Quaternion](http://en.wikipedia.org/wiki/Quaternions)
- [三维旋转矩阵课件](http://wenku.baidu.com/view/58b1f64cf7ec4afe04a1df73.html)
- [[转载]三维旋转矩阵实用算法 with Detail illustrations](http://blog.sciencenet.cn/blog-254499-737232.html)
- [Rotation Matrix](http://en.wikipedia.org/wiki/Rotation_matrix) (this wiki is long but worth the time)
- [Rotation vectors vs quaternions](http://stackoverflow.com/questions/10926546/rotation-vectors-vs-quaternions) (Good article!)
- [Quaternions to Rotation Angles](http://www.mathworks.com/help/aeroblks/quaternionstorotationangles.html)
- [Tutorial 17 : Rotations in OpenGL](http://www.opengl-tutorial.org/intermediate-tutorials/tutorial-17-quaternions/)(If you want to read only one article regarding that problem, that's the one!)
- [Relative Rotation Between two Quaternions](http://answers.ros.org/question/10124/relative-rotation-between-two-quaternions/)
- ['Difference' between two quaternions](http://stackoverflow.com/questions/1755631/difference-between-two-quaternions)
- [3D transformations. Quaternion -> <-Euler Angle](http://stackoverflow.com/questions/11103683/euler-angle-to-quaternion-then-quaternion-to-euler-angle)





##Randomness

- [How to verify randomness](http://www.guokr.com/question/438291/)



## Codes

```
//Quaternion code examples.

import java.util.Arrays;

public class Quaternion {

	 private double w, x, y, z; 

	    // create a new object with the given components
	    public Quaternion(double x0, double x1, double x2, double x3) {
	        this.w = x0;
	        this.x = x1;
	        this.y = x2;
	        this.z = x3;
	    }
	    
	    public float[] getData(){
	    	float[] data = new float[4];
	    	data[0] = (float)w;
	    	data[1] = (float)x;
	    	data[2] = (float)y;
	    	data[3] = (float)z;
	    	return data;
	    }

	    // return a string representation of the invoking object
	    public String toString() {
	        return w + " + " + x + "i + " + y + "j + " + z + "k";
	    }

	    // return the quaternion norm
	    public double norm() {
	        return Math.sqrt(w*w + x*x +y*y + z*z);
	    }
	    
	    public void normalize(){
	    	double norm = this.norm();
	    	w /= norm;
	    	x /= norm;
	    	y /= norm;
	    	z /= norm;
	    }

	    // return the quaternion conjugate
	    public Quaternion conjugate() {
	        return new Quaternion(w, -x, -y, -z);
	    }

	    // return a new Quaternion whose value is (this + b)
	    public Quaternion plus(Quaternion b) {
	        Quaternion a = this;
	        return new Quaternion(a.w+b.w, a.x+b.x, a.y+b.y, a.z+b.z);
	    }


	    // return a new Quaternion whose value is (this * b)
	    public Quaternion times(Quaternion b) {
	        Quaternion a = this;
	        double y0 = a.w*b.w - a.x*b.x - a.y*b.y - a.z*b.z;
	        double y1 = a.w*b.x + a.x*b.w + a.y*b.z - a.z*b.y;
	        double y2 = a.w*b.y - a.x*b.z + a.y*b.w + a.z*b.x;
	        double y3 = a.w*b.z + a.x*b.y - a.y*b.x + a.z*b.w;
	        return new Quaternion(y0, y1, y2, y3);
	    }

	    // return a new Quaternion whose value is the inverse of this
	    public Quaternion inverse() {
	        double d = w*w + x*x + y*y + z*z;
	        return new Quaternion(w/d, -x/d, -y/d, -z/d);
	    }


	    // return a / b
	    public Quaternion divides(Quaternion b) {
	         Quaternion a = this;
	        return a.inverse().times(b);
	    }

	    // returan difference between this and target quaternion
	    public Quaternion rotateto(Quaternion b){
	    	Quaternion a = this;
			Quaternion transition = a.times(b.inverse());
			return transition;
	    }
	    
	    /**
         * Converts this Quaternion to Euler rotation angles {@code roll}, {@code
         * pitch} and {@code yaw} in radians.
         * {@link #fromEulerAngles(float, float, float)} performs the inverse
         * operation. The code was adapted from:
         * http://www.euclideanspace.com/maths/geometry
         * /rotations/conversions/quaternionToEuler/index.htm.
         * <p>
         * <b>Attention:</b> This method assumes that this Quaternion is normalized.
         *
         * @return the PVector holding the roll (x coordinate of the vector), pitch (y
         *         coordinate of the vector) and yaw angles (z coordinate of the
         *         vector). <b>Note:</b> The order of the rotations that would produce
         *         this Quaternion (i.e., as with {@code fromEulerAngles(roll, pitch,
         *         yaw)}) is: y->z->x.
         *
         * @see #fromEulerAngles(float, float, float)
         */

        public double[] eulerAngles() {
        	double[] euler = new double[3];
            double roll, pitch, yaw;
            double test = (x * y + z * w);
            if (test > 0.499) { // singularity at north pole
                    pitch = 2 * Math.atan2(x, w);
                    yaw = Math.PI / 2;
                    roll = 0;
                    euler[0] = roll;
                    euler[1] = pitch;
                    euler[2] = yaw;
                    return euler;
            }
            if (test < -0.499) { // singularity at south pole
                    pitch = -2 * Math.atan2(x, w);
                    yaw = -Math.PI / 2;
                    roll = 0;
                    euler[0] = roll;
                    euler[1] = pitch;
                    euler[2] = yaw;
                    return euler;
            }
            double sqx = x * x;
            double sqy = y * y;
            double sqz = z * z;
            pitch = Math.atan2(2 * y * w - 2 * x * z, 1 - 2 * sqy - 2 * sqz);
            yaw = Math.asin(2 * test);
            roll = Math.atan2(2 * x * w - 2 * y * z, 1 - 2 * sqx - 2 * sqz);
            euler[0] = roll;
            euler[1] = pitch;
            euler[2] = yaw;
            return euler;            
    }


    private static void getQuaternionFromEuler(double roll, double pitch, double yaw, double[] quaternion){
    	double s1 = Math.sin(yaw/2);	
    	double s2 = Math.sin(pitch/2);	
    	double s3 = Math.sin(roll/2);	
    	
    	double c1 = Math.cos(yaw/2);
    	double c2 = Math.cos(pitch/2);
    	double c3 = Math.cos(roll/2);

    	quaternion[0] =  c1*c2*c3 - s1*s2*s3; //w 
    	quaternion[1] =  s1*s2*c3 + c1*c2*s3; //x
    	quaternion[2] =  s1*c2*c3 + c1*s2*s3; //y
    	quaternion[3] =  c1*s2*c3 - s1*c2*s3; //z
    }

	    // sample client for testing
	    public static void main(String[] args) {
	        Quaternion a = new Quaternion(0.5, 1.0, 0.0, 0.0);
			a.normalize();
	        System.out.println("a = " + a);

	        Quaternion b = new Quaternion(0.0, 5.0, 1.0, -2.0);
	        System.out.println("b = " + b);

	        System.out.println("norm(a)  = " + a.norm());
	        System.out.println("conj(a)  = " + a.conjugate());
	        System.out.println("a + b    = " + a.plus(b));
	        System.out.println("a * b    = " + a.times(b));
	        System.out.println("b * a    = " + b.times(a));
	        System.out.println("a / b    = " + a.divides(b));
	        System.out.println("a^-1     = " + a.inverse());
	        System.out.println("a^-1 * a = " + a.inverse().times(a));
	        System.out.println("a * a^-1 = " + a.times(a.inverse()));
	        System.out.println("euler angle(a) = " + Arrays.toString(a.eulerAngles()));
			double[] quaternion = new double[4];
			getQuaternionFromEuler(a.eulerAngles()[0], a.eulerAngles()[1], a.eulerAngles()[2], quaternion);
			System.out.println("back to quaternion from euler angle(a) = " + Arrays.toString(quaternion));
	        
		}

		public void setQuaternion(double x0, double x1, double x2, double x3) {
	        this.w = x0;
	        this.x = x1;
	        this.y = x2;
	        this.z = x3;
	    }

}


```



