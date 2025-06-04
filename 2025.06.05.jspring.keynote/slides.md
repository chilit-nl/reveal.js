<img src="./Chilit%20logo%20kleur.svg" height="100" />
<img style="margin-left: 2em;" src="./JSPRING-2025_rgb-0021.png" height="200" />

## Are you addicted to your framework? I was too, let's go to rehab together.

---

<img src="old-man-yells-at-cloud.png" class="stretch">
<!--* Connection to SOLID principles
* Separate components that change for different reasons (SRP)
* Connection to DIP-->

---

<div style="display: flex; gap: 50px">
    <img src="./profile.jpeg" height="400" width="400" />
    <div style="display: flex; flex-direction: column; justify-content: center; text-align: left;">
        <div>
            John Sterken<br />
            Software Engineer<br />
            <br/>
            <img src="./Chilit%20logo%20kleur.svg" height="48" />
        </div>
    </div>
</div>

---

## Should I abandon my framework altogether?

<!-- .slide: class="fragmented-lists" -->
* Of course not; frameworks are great!
* But stay SOLID

---

## Why is this important?

<!-- .slide: class="fragmented-lists" -->
* As developers, we are all architects
* Maximize decisions not made
* Single reason for change (SRP)
<!-- * Framework dependency shuts down options -->

---

---

```java
package com.example.service;

import org.springframework.stereotype.Service;

@Service
public class SimpleService {
    private final ApiClient feignClient;
    
    public SimpleService(ApiClient feignClient) {
        this.feignClient = feignClient;
    }

    public String callExternalService() {
        return feignClient.getExternalData();
    }
}
```

---

```java
package com.example.service;

import org.springframework.stereotype.Service;
import com.netflix.hystrix.contrib.javanica.annotation.HystrixCommand;

@Service
public class SimpleService {
    // feignClient, constructor
    @HystrixCommand(fallbackMethod = "fallbackResponse")
    public String callExternalService() {
        return feignClient.getExternalData();
    }

    public String fallbackResponse() {
        return "Fallback response";
    }
}

```

---

<img src="maintenance_mode.png" class="stretch" />

---

# Spring example application

---

<img src="old-architecture/without-framework.png" alt="img.png" class="stretch" />

---

<img src="old-architecture/with-framework.png" alt="img.png" class="stretch" />

---

```java[|4|10]
package com.example.service;

...
import org.springframework.stereotype.Service;
...

@Service
@Transactional
public class SomeService {
    private final SomeRepository someRepository;

    // constructor, other methods, etc.
    
    public void doSomething() {
        SomeEntity entity = someRepository.findById(...);
        ...
    }
}
```

---

```java[|4]
package com.example.repository;

...
import org.springframework.data.jpa.repository.JpaRepository;
...

public interface SomeRepository extends JpaRepository<SomeEntity, Long> {
    // custom query methods
}
```

---

## How do we decouple?

<!-- .slide: class="fragmented-lists" -->
* Separate your core logic from the framework
* We can use the D from the SOLID principles (Dependency Inversion Principle)

---

## What is your core domain?

---

## core domain != database tables

---

## core domain == model of reality

---

## Refactored example


<img src="refactored.png" alt="img.png" class="stretch" />

---

<div class="stretch" style="display: flex; justify-content: center; align-items: center; width: 100%">
<div style="flex-grow: 2">

```java
package com.example.domain;

// only imports that start with java

public record SomeEntity (UUID id, ...) {
}
```

</div>
<img src="new-architecture/domain.png" alt="img.png" class="stretch side-image" />
</div>

---

<div class="stretch" style="display: flex; justify-content: center; align-items: center; width: 100%">
<div style="flex-grow: 2">

```java[|3-4]
package com.example.domain.repository;

import com.example.domain.SomeEntity;
// imports from java

public interface SomeRepository {
    Optional<SomeEntity> findById(UUID id);
}
```

</div>
    <img src="new-architecture/dai.png" alt="img.png" class="stretch side-image" />
</div>

---

<div class="stretch" style="display: flex; justify-content: center; align-items: center; width: 100%">
<div style="flex-grow: 2">

```java[|3-5]
package com.example.service;

import com.example.domain.SomeEntity;
import com.example.domain.repository.SomeRepository;
// imports from java

public class SomeService {
    private final SomeRepository someRepository;

    // constructor, other methods, etc.
    
    public void doSomething() {
        SomeEntity entity = someRepository
            .findById(...);
        ...
    }
}
```

</div>
    <img src="new-architecture/service.png" alt="img.png" class="stretch side-image" />
</div>

---

<div class="stretch" style="display: flex; justify-content: center; align-items: center; width: 100%">
<div style="flex-grow: 2">

```java
package com.example.jpa.repository;

// imports

public interface SomeJpaRepository
        extends JpaRepository<SomeJpaEntity, Long> {
    
    Optional<SomeJpaEntity> findById(UUID id);
    // custom query methods
}
```

</div>
    <img src="new-architecture/jpa.png" alt="img.png" class="stretch side-image" />
</div>

---

<div class="stretch" style="display: flex; justify-content: center; align-items: center; width: 100%">
<div style="flex-grow: 2">

```java
package com.example.jpa.entity;

// imports

@Entity
public class SomeJpaEntity {
    @Id
    @GeneratedValue
    private UUID id;

    // other fields, getters, setters, etc.
}
```

</div>
    <img src="new-architecture/database.png" alt="img.png" class="stretch side-image" />
</div>

---

<div class="stretch" style="display: flex; justify-content: center; align-items: center; width: 100%">
<div style="flex-grow: 2">

```java
package com.example.jpa.dao;

// imports

public class SomeRepositoryJpaDao 
        implements SomeRepository {
    private final SomeJpaRepository someJpaRepository;

    @Override
    public Optional<SomeEntity> findById(UUID id) {
        return someJpaRepository.findById(id)
            .map(...);
    }
}
```

</div>
    <img src="new-architecture/dao.png" alt="img.png" class="stretch side-image" />
</div>

---

<div class="stretch" style="display: flex; justify-content: center; align-items: center; width: 100%">
<div style="flex-grow: 2">

```java
package com.example.config;

// imports 

@Configuration
public class Config {
  @Bean
  public SomeService someService(SomeRepository repo) {
    return new SomeService(repo);
  }
    
  @Bean
  public SomeRepository someRepository(
      SomeJpaRepository repo) {
    return new SomeRepositoryJpaDao(repo);
  }
}
```

</div>
    <img src="new-architecture/framework.png" alt="img.png" class="stretch side-image" />
</div>

---

# Conclusion

<!-- .slide: class="fragmented-lists" -->
* Frameworks are great, but don't let them dictate your architecture
* Keep your core domain and logic independent
* Use the Dependency Inversion Principle to separate concerns

---

## CHILIT @ J-Spring 2025

### Spice, waffles, fun and games!

<img src="./stand/wafels.png" height="300" style="float: left" />
<img src="./stand/stand.png" height="300" style="float: right" />
