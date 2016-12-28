---
layout: page
title: Bridge
permalink: /patterns/Bridge/
tag: pattern
---

* [Story](#Story)
* [UML](#UML)
* [Implementation](#Implementation)
* [Usage](#Usage)


###  <a id="Story"></a>Story 

Decouple an abstraction from its implementation so that the two can vary independently.

Steering wheel is an example of the Bridge.
The purpose of a steering wheel is to transmit  driver's input to the steered wheels in order to dynamically change direction of the vehicle.
There are different implementations of the steering wheels used in cars, buses, tracks, tractors and formulas.




###  <a id="UML"></a>UML 
[![]({{site.baseurl}}/assets/img/bridge.png)]({{site.baseurl}}/assets/img/bridge.png)

###  <a id="Implementation"></a>Implementation 

#### *Implementor.java* 
```java 
package com.hundredwordsgof.bridge;

/**
 * 
 * Implementor, defines interface for implementation
 *
 */
public interface Implementor {

	void implementation();
	
}
```

#### *ConcreteImplementorA.java* 
```java 
package com.hundredwordsgof.bridge;

/**
 * 
 * ConcreteImplementatorA, implements Implementor interface
 *
 */
public class ConcreteImplementorA implements Implementor {


	public void implementation() {
	}

}
```

#### *ConcreteImplementorB.java* 
```java 
package com.hundredwordsgof.bridge;

/**
 * 
 * ConcreteImplementatorB, implements Implementor interface
 *
 */
public class ConcreteImplementorB implements Implementor {


	public void implementation() {
	}

}
```

#### *RefinedAbstraction.java* 
```java 
package com.hundredwordsgof.bridge;

/**
 * 
 * Refined Abstraction, extends the interface defined by Abstraction
 *
 */
public class RefinedAbstraction extends Abstraction{

	public RefinedAbstraction(Implementor implementor) {
		super(implementor);
	}

	public String operation() {
		return this.implementor.getClass().getName();
	}

}
```

#### *Abstraction.java* 
```java 
package com.hundredwordsgof.bridge;


/**
 * 
 * Abstraction, defines abstraction interface, maintains a reference to object of type Implementator
 * 
 */
abstract class Abstraction {

	protected Implementor implementor;
	
	public Abstraction(Implementor implementor){
		this.implementor = implementor;		
	}
	
	abstract String operation();
	
}
```

###  <a id="Usage"></a>Usage 

#### *BridgeTest.java* 
```java 
package com.hundredwordsgof.bridge;

import static org.junit.Assert.*;

import org.junit.Test;

/**
 * Test implementation of the Bridge pattern.
 */
public class BridgeTest {

	@Test
	public void testBuilder(){

		// creates refined abstraction with concreteimplementorA
		RefinedAbstraction refinedAbstractionA = new RefinedAbstraction(new ConcreteImplementorA());
		//invokes operation
		assertEquals("com.hundredwordsgof.bridge.ConcreteImplementorA", refinedAbstractionA.operation());
		
		// creates refined abstraction with concreteimplementorB
		RefinedAbstraction refinedAbstractionB = new RefinedAbstraction(new ConcreteImplementorB());
		//invokes operation
		assertEquals("com.hundredwordsgof.bridge.ConcreteImplementorB", refinedAbstractionB.operation());
		
	}	
}
```
