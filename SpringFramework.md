# Spring Framework Cheat Sheet

TBD

## Contents

#### [Concepts](#concepts-1)

1. [Dependency Injection](#dependency-injection)
1. [Inversion of Control (IoC)](#inversion-of-control-ioc)

## Concepts

### Dependency Injection

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

### Inversion of Control (IoC)

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

---

1. TBD Inversion of Control
1. TBD Bean Scope
1. TBD Spring Bean Life Cycle

## References

1. [Dependency Injection](https://docs.spring.io/spring-framework/reference/core/beans/dependencies/factory-collaborators.html)
