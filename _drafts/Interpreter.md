---
layout: page
title: Interpreter
permalink: /Interpreter/
tag: pattern
---



### Story 

A person who translates orally from one language into another.



### UML 
![]({{site.baseurl}}/assets/img/interpreter.png)

#### *AbstractExpression.java* 
```java 
package com.hundredwordsgof.interpreter;

/**
 * 
 * AbstractExpresion defines interface for interpretation.
 * Interface must be used by TerminalEpression and NonTerminalEpression.
 *
 */
public abstract class AbstractExpression {

	abstract void interpret(Context context);
	
}
```

#### *AndExpression.java* 
```java 
package com.hundredwordsgof.interpreter;

import java.util.List;


/**
 * 
 * AndExpression implements AbstractExpression for logical AND grammar expression.
 *
 */
public class AndExpression extends AbstractExpression {

	private AbstractExpression firstAbstractExpression;
	private AbstractExpression secondAbstractExpression;
	
	public AndExpression(AbstractExpression firstAbstractExpression, AbstractExpression secondAbstractExpression){
		this.firstAbstractExpression = firstAbstractExpression;
		this.secondAbstractExpression = secondAbstractExpression;
	}
	
	public void interpret(Context context) {
		
		firstAbstractExpression.interpret(context);
		secondAbstractExpression.interpret(context);
		
		List<Boolean> operands = context.getOperands();
				
		Boolean firstOperand = operands.get(0);		
		Boolean secondOperand = operands.get(1);
	
		Boolean result = firstOperand &&  secondOperand;
		context.setResult(result);
				
	}

	
	
}
```

#### *Context.java* 
```java 
package com.hundredwordsgof.interpreter;

import java.util.ArrayList;
import java.util.List;

/**
 * 
 * Context contains global informations for Interpreter.
 *
 */
public class Context {

	// holds a list of operands which are in fact TerminalExpressions
	private List<Boolean> operands = new ArrayList<Boolean>();
	
	// holds result of expression 
	private Boolean result = null;
	
	public List<Boolean> getOperands() {
		return operands;
	}

	public void addOperand(Boolean operand){
		operands.add(operand);
	}
	
	public boolean isResult() {
		return result;
	}

	public void setResult(Boolean result) {
		this.result = result;
	}
	
}
```

#### *OrExpression.java* 
```java 
package com.hundredwordsgof.interpreter;

import java.util.List;

/**
 * 
 * OrExpression implements AbstractExpression for logical OR grammar expression.
 *
 */
public class OrExpression extends AbstractExpression{

	private AbstractExpression firstAbstractExpression;
	private AbstractExpression secondAbstractExpression;
	
	public OrExpression(AbstractExpression firstAbstractExpression, AbstractExpression secondAbstractExpression){
		this.firstAbstractExpression = firstAbstractExpression;
		this.secondAbstractExpression = secondAbstractExpression;
	}
	
	public void interpret(Context context) {
		
		firstAbstractExpression.interpret(context);
		secondAbstractExpression.interpret(context);
		
		List<Boolean> operands = context.getOperands();
				
		Boolean firstOperand = operands.get(0);		
		Boolean secondOperand = operands.get(1);
	
		Boolean result = firstOperand || secondOperand;
		context.setResult(result);
				
	}
}
```

#### *TerminalExpression.java* 
```java 
package com.hundredwordsgof.interpreter;

/**
 * 
 * TerminalExpresion implements AbstractExpression for literal  symbol in grammar.
 *
 */
public class TerminalExpression extends AbstractExpression {

	private boolean data;
	
	public TerminalExpression(boolean data){
		this.data = data;
	}
	
	public void interpret(Context context) {
		// add operand to context
		context.addOperand(this.data);
	}

}
```
