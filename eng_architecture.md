Architecture about productivity
===========



#### Macro

- [Pinterest Architecture Update - 18 Million Visitors, 10x Growth,12 Employees, 410 TB Of Data](http://highscalability.com/blog/2012/5/21/pinterest-architecture-update-18-million-visitors-10x-growth.html)
	- use python and django in the smart wyas.
	
- [Quip: What we learned from building Quip on 8 different platforms with only 14 engineers](https://quip.com/blog/building-great-products-with-small-teams)
	- build once, use multiple times, invest heavily in tooling.

- [Quip: React with C++: Building the Quip Mac and Windows Apps](https://medium.com/@btaylor/react-with-c-building-the-quip-mac-and-windows-apps-c63155c1531b#.g58jbt64d)




### Beyond system

- [how advertising works today](http://www.displayadtech.com/the_display_advertising_technology_landscape)


###  Design pattern

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