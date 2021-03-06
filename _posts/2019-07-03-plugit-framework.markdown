---
layout: post
title:  "Plugit Framework"
subtitle: "Apex framework for building modular plugits"
author_name: "@svshrikhande"
avatar: "http://swapnilshrikhande.in/assets/img/swapnil-shrikhande.jpg"
image: "/img/plugit_framework.jpg"
date:   2017-07-03 03:26:00
category: 'Apex Framework'
tags: 'Salesforce'
---

# Plugit : A Module Framework For Apex 

Ever wondered if the apex software blocks can be easily installed and plugged in into each other ?
- Plugit tries to solve above problem by providing a base framework to design services which can be combined together using a keyword driven approach.
- Implements [Fluent Interface](https://en.wikipedia.org/wiki/Fluent_interface) 

## Installation
- Managed Package (1.1 beta) : [Installation Link](https://login.salesforce.com/packaging/installPackage.apexp?p0=04t2v000000sxpX)
- Source Code : [https://github.com/swapnilshrikhande/plugit-core-apex](https://github.com/swapnilshrikhande/plugit-core-apex)


## Key Features
- Develop modular and interoperable apex services called as plugits 
- Supports extensible service factory to add custom service factory
- All default methods can be overriden to extend the framework
- Use pipe keyword to easily chain multiple plugits like below

### typical usage example
```java
// load QueryAccounts plugit and pipe its output to next plugit and so on

Pluggable resultPlug = plugin('QueryAccounts')
    .exec( seedData)
    .pipe('ProcessActiveAccounts')
    .pipe('NotifyInActiveAccountOwners')
    .pass('HandleAccountSuccess')
    .fail('SendEmailToAdmin') //invoked if any of the plugit fails
    .fail('LogDebugToFile');

if( resultPlug.hasErrors() ){
    //access resultPlug.errors();
} else {
   Object result  = resultPlug.result();
}

```

## Complete Sample Usage

### Extend ```Plug``` base class
```java
public class Calculator extends Plug {
	
    public override Object execute(Object data) {
        
        Pluggable addService = plugin('AdditionService')
            .exec( data )
            .pass( 'AdditionServicePassed' )
            .fail( 'AdditionServiceFailed' );

        Object resultValue = addService.result();

        if(  resultValue == null ){
        	System.debug( 'Errors In The Service '+addService.errors());
        }

        return resultValue;
    }
}

public class AdditionService extends Plug {
    public override Object execute(Object data) {

        Map<String,Decimal> dataMap = (Map<String,Decimal>)data;

        try {
            no1 = Integer.valueOf(dataMap.get('no1'));
            no2 = Integer.valueOf(dataMap.get('no2'));

            output('result',no1+no2);
            
            return no1+no2;

        } catch (Exception exp){
            //sets error state
            error('AdditionServiceException',exp);
        }
        
        return null;
    }
}

public class AdditionServicePassed extends Plug {

	public override Object execute(Object data) {

        System.debug(' outputResult ='+Decimal.valueOf(data));

        return data;
    }
}


public class AdditionServiceFailed extends Plug {

	public override Object execute(Object data) {

        //handle errors errors
        for( String errorKey : this.errors().keySet() ) {
        	System.debug(errorKey +' : '+ ((Exception)errors.get(errorKey)) );
            //handle errors here
        }

        return null;
    }
}

```

### Invoke as a normal class or from another Plugit

#### Normal Class : 
```java
Object result = Plug.plugin('CalculatorNanoService')
                    .exec(new Map<String,Decimal>{
                        'no1' => 1,
                        'no2' => 50
                    });

```

#### Another Plugit : 
```java
plugin('CalculatorNanoService')
      .exec(new Map<String,Decimal>{
	    'no1' => 1,
	    'no2' => null
      });
```

### References
- [https://en.wikipedia.org/wiki/Fluent_interface](https://en.wikipedia.org/wiki/Fluent_interface)
- [https://martinfowler.com/bliki/FluentInterface.html](https://martinfowler.com/bliki/FluentInterface.html)






