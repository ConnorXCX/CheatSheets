# Spring Framework

## Contents

#### [Concepts](#concepts-1)

1. [Inversion of Control (IoC)](#inversion-of-control-ioc)
1. [Dependency Injection](#dependency-injection)
1. [Spring Beans](#spring-beans)

## Concepts

### Inversion of Control (IoC)

- Inversion of Control (IoC) is a design principle in which the control of object creation and dependency management is transferred from the application code to the Spring framework. In the context of Spring, this means that the framework is responsible for instantiating, configuring, and managing the lifecycle of objects (also called beans), instead of the developer manually creating them. This is typically achieved through the Spring IoC container, which uses configuration metadata (XML, annotations, or Java-based configuration) to know how to assemble application objects.
- Dependency injection (DI) is a specialized form of IoC, whereby objects define their dependencies (that is, the other objects they work with) only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method. The IoC container then injects those dependencies when it creates the bean. This process is fundamentally the inverse (hence the name, Inversion of Control) of the bean itself controlling the instantiation or location of its dependencies by using direct construction of classes or a mechanism such as the Service Locator pattern.
- In Spring, the objects that form the backbone of your application and that are managed by the Spring IoC container are called beans.
- A bean is an object that is instantiated, assembled, and managed by a Spring IoC container. Otherwise, a bean is simply one of many objects in your application.
- Beans, and the dependencies among them, are reflected in the configuration metadata used by a container.
- The `org.springframework.beans` and `org.springframework.context` packages are the basis for Spring Framework’s IoC container.
- The `BeanFactory` interface provides an advanced configuration mechanism capable of managing any type of object. `ApplicationContext` is a sub-interface of `BeanFactory`. It adds:
  - Easier integration with Spring’s AOP features
  - Message resource handling (for use in internationalization)
  - Event publication
  - Application-layer specific contexts such as the `WebApplicationContext` for use in web applications.
- In short, the `BeanFactory` provides the configuration framework and basic functionality, and the `ApplicationContext` adds more enterprise-specific functionality. The `ApplicationContext` is a complete superset of the `BeanFactory` and is used exclusively in this chapter in descriptions of Spring’s IoC container.

### Dependency Injection

- Dependency Injection is a specific type of Inversion of Control where the dependencies of a class are provided externally rather than the class creating them itself. In Spring, DI allows you to inject dependencies (like service or repository classes) into your components (like controllers or other services), either through constructor injection, setter injection, or field injection. This promotes loose coupling, enhances testability, and improves code maintainability.
- Inversion of Control (IoC) is the broader principle where the control of object creation is handed over to the Spring framework. Dependency Injection (DI) is the mechanism Spring uses to implement IoC — it injects the required dependencies into a class, rather than the class creating those dependencies itself. This allows for greater decoupling of components, easier testing, and more maintainable code. Spring supports DI via annotations (`@Autowired`, `@Inject`), XML configuration, or Java-based configuration.
- Dependency injection, an aspect of Inversion of Control (IoC), is a general concept stating that we do not create our objects manually but instead describe how they should be created. Then an IoC container will instantiate required classes if needed.
- Dependency injection (DI) is a process whereby objects define their dependencies (that is, the other objects with which they work) only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method. The container then injects those dependencies when it creates the bean. - This process is fundamentally the inverse (hence the name, Inversion of Control) of the bean itself controlling the instantiation or location of its dependencies on its own by using direct construction of classes or the Service Locator pattern.
- Code is cleaner with the DI principle, and decoupling is more effective when objects are provided with their dependencies. The object does not look up its dependencies and does not know the location or class of the dependencies. As a result, your classes become easier to test, particularly when the dependencies are on interfaces or abstract base classes, which allow for stub or mock implementations to be used in unit tests.
- Dependency injection exists in two major variants: Constructor-based dependency injection and Setter-based dependency injection:

  1.  **Constructor-based Dependency Injection**

      - Constructor-based DI is accomplished by the container invoking a constructor with a number of arguments, each representing a dependency. Calling a `static` factory method with specific arguments to construct the bean is nearly equivalent, and this discussion treats arguments to a constructor and to a `static` factory method similarly. The following example shows a class that can only be dependency-injected with constructor injection:

      ```java
      public class SimpleMovieLister {

         // the SimpleMovieLister has a dependency on a MovieFinder
         private final MovieFinder movieFinder;

         // a constructor so that the Spring container can inject a MovieFinder
         public SimpleMovieLister(MovieFinder movieFinder) {
            this.movieFinder = movieFinder;
         }

         // business logic that actually uses the injected MovieFinder is omitted...
      }
      ```

  1.  **Setter-based Dependency Injection**

      - Setter-based DI is accomplished by the container calling setter methods on your beans after invoking a no-argument constructor or a no-argument `static` factory method to instantiate your bean.
      - The following example shows a class that can only be dependency-injected by using pure setter injection. This class is conventional Java. It is a POJO that has no dependencies on container specific interfaces, base classes, or annotations.

      ```java
      public class SimpleMovieLister {

         // the SimpleMovieLister has a dependency on the MovieFinder
         private MovieFinder movieFinder;

         // a setter method so that the Spring container can inject a MovieFinder
         public void setMovieFinder(MovieFinder movieFinder) {
            this.movieFinder = movieFinder;
         }

         // business logic that actually uses the injected MovieFinder is omitted...
      }
      ```

### Spring Beans

### Overview

Within the container itself, these bean definitions are represented as `BeanDefinition` objects, which contain (among other information) the following metadata:

- A package-qualified class name: typically, the actual implementation class of the bean being defined.
- Bean behavioral configuration elements, which state how the bean should behave in the container (scope, lifecycle callbacks, and so forth).
- References to other beans that are needed for the bean to do its work. These references are also called collaborators or dependencies.
- Other configuration settings to set in the newly created object — for example, the size limit of the pool or the number of connections to use in a bean that manages a connection pool.

This metadata translates to a set of properties that make up each bean definition. The following table describes these properties:

| Property                 |
| ------------------------ |
| Class                    |
| Name                     |
| Scope                    |
| Constructor Arguments    |
| Properties               |
| Autowiring mode          |
| Lazy initialization mode |
| Initialization method    |
| Destruction method       |

#### Bean Scopes

| Scope       | Description                                                                                                                                                                                                                                                  |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| singleton   | (Default) Scopes a single bean definition to a single object instance for each Spring IoC container.                                                                                                                                                         |
| prototype   | Scopes a single bean definition to any number of object instances.                                                                                                                                                                                           |
| request     | Scopes a single bean definition to the lifecycle of a single HTTP request. That is, each HTTP request has its own instance of a bean created off the back of a single bean definition. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| session     | Scopes a single bean definition to the lifecycle of an HTTP `Session`. Only valid in the context of a web-aware Spring `ApplicationContext`.                                                                                                                 |
| application | Scopes a single bean definition to the lifecycle of a `ServletContext`. Only valid in the context of a web-aware Spring `ApplicationContext`.                                                                                                                |
| websocket   | Scopes a single bean definition to the lifecycle of a `WebSocket`. Only valid in the context of a web-aware Spring `ApplicationContext`.                                                                                                                     |

#### Life Cycle

The lifecycle of a Spring bean consists of the following phases, which are listed below

1. **Container Started**: The Spring IoC container is initialized.
1. **Bean Instantiated**: The container creates an instance of the bean.
1. **Dependencies Injected**: The container injects the dependencies into the bean.
1. **Custom init() method**: If the bean implements InitializingBean or has a custom initialization method specified via `@PostConstruct` or init-method.
1. **Bean is Ready**: The bean is now fully initialized and ready to be used.
1. **Custom utility method**: This could be any custom method you have defined in your bean.
1. **Custom destroy() method**: If the bean implements DisposableBean or has a custom destruction method specified via `@PreDestroy` or destroy-method, it is called when the container is shutting down.

## References

1. [Dependency Injection](https://docs.spring.io/spring-framework/reference/core/beans/dependencies/factory-collaborators.html)
1. [Bean Scopes](https://docs.spring.io/spring-framework/reference/core/beans/factory-scopes.html)
1. [Bean Life Cycle in Java Spring](https://www.geeksforgeeks.org/java/bean-life-cycle-in-java-spring/)
