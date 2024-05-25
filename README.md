Sure, here is the entire program consolidated into a single file. This approach is useful for simplicity and quick testing. 

```java
package com.example.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;

@SpringBootApplication
public class DemoApplication implements CommandLineRunner {

    @Autowired
    private MySingletonBean mySingletonBean1;

    @Autowired
    private MySingletonBean mySingletonBean2;

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Override
    public void run(String... args) throws Exception {
        System.out.println("mySingletonBean1: " + mySingletonBean1);
        System.out.println("mySingletonBean2: " + mySingletonBean2);
    }

    @Configuration
    public static class AppConfig {

        @Bean
        @Scope("singleton")
        public MySingletonBean mySingletonBean() {
            return new MySingletonBean();
        }
    }

    public static class MySingletonBean {

        public MySingletonBean() {
            System.out.println("MySingletonBean instance created");
        }
    }
}
```

In this single file:
1. `DemoApplication` class contains the main method to start the Spring Boot application and implements `CommandLineRunner` to execute code after the application starts.
2. The `AppConfig` class is nested within `DemoApplication` and defines the singleton-scoped bean.
3. The `MySingletonBean` class is also nested within `DemoApplication` and contains the constructor that prints a message when an instance is created.

To run this program, simply place this file in the appropriate package directory (`com/example/demo`) and execute it as a Spring Boot application. You should see the output demonstrating that the `MySingletonBean` instance is created only once.
Sure! Here's a complete Spring application demonstrating the use of a prototype-scoped bean, all in a single file:

```java
package com.example.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;

@SpringBootApplication
public class DemoApplication implements CommandLineRunner {

    @Autowired
    private MyPrototypeBean myPrototypeBean1;

    @Autowired
    private MyPrototypeBean myPrototypeBean2;

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Override
    public void run(String... args) throws Exception {
        System.out.println("myPrototypeBean1: " + myPrototypeBean1);
        System.out.println("myPrototypeBean2: " + myPrototypeBean2);
    }

    @Configuration
    public static class AppConfig {

        @Bean
        @Scope("prototype")
        public MyPrototypeBean myPrototypeBean() {
            return new MyPrototypeBean();
        }
    }

    public static class MyPrototypeBean {

        public MyPrototypeBean() {
            System.out.println("MyPrototypeBean instance created");
        }
    }
}
```

In this single file:
1. The `DemoApplication` class contains the main method to start the Spring Boot application and implements `CommandLineRunner` to execute code after the application starts.
2. The `AppConfig` class is nested within `DemoApplication` and defines the prototype-scoped bean.
3. The `MyPrototypeBean` class is also nested within `DemoApplication` and contains the constructor that prints a message when an instance is created.

To run this program, simply place this file in the appropriate package directory (`com/example/demo`) and execute it as a Spring Boot application. You should see the output demonstrating that a new `MyPrototypeBean` instance is created each time it is requested, showing different hash codes for `myPrototypeBean1` and `myPrototypeBean2`.

```
MyPrototypeBean instance created
MyPrototypeBean instance created
myPrototypeBean1: com.example.demo.DemoApplication$MyPrototypeBean@<hashcode1>
myPrototypeBean2: com.example.demo.DemoApplication$MyPrototypeBean@<hashcode2>
```

This output confirms that two separate instances of `MyPrototypeBean` are created, which is the expected behavior for a prototype-scoped bean.
