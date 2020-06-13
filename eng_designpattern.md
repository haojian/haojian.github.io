Design pattern
===========

- [Joshua Bloch: Bumper-Sticker API Design](https://www.infoq.com/articles/API-Design-Joshua-Bloch/)
	- Video: [How to Design a Good API & Why it Matters](http://www.infoq.com/presentations/effective-api-design)


** Singleton Pattern **

```
public class Singleton {
	// Private constructor prevents instantiation from other classes
	private Singleton() { }
 
	/**
	* SingletonHolder is loaded on the first execution of Singleton.getInstance() 
	* or the first access to SingletonHolder.INSTANCE, not before.
	*/
	private static class SingletonHolder { 
		private static final Singleton INSTANCE = new Singleton();
	}
 
	public static Singleton getInstance() {
		return SingletonHolder.INSTANCE;
	}
}
```
