<!-- .slide: data-background-image="jfall_intro.png" -->

---

## Gargage Collectors <!-- .element: style="margin-bottom: 300px" -->
Gargabe in... gargabe out.
<!-- .slide: data-background-image="pexels-lenin-estrada-2569997.jpg" -->

---

<div style="display: flex; gap: 50px">
  <img src="./profile.jpg" height="400px" width="400px" style="border: 5px solid; border-image-source: linear-gradient(-45deg, #FFC796 0%, #FF6B95 100%); border-image-slice: 1;" />
  <div style="display: flex; flex-direction: column; justify-content: center; text-align: left;">
    <div>
      Lennart ten Wolde<br />
      Software Engineer, CHILIT
    </div>
    <div style="margin-top: 50px">
      KPN IoT<br/>
      Backend Java Development
    </div>
  </div>
</div>

---

## Agenda

<!-- .slide: class="fragmented-lists" -->
- JVM
- Memory management
- Garbage collection
- JVM GC timeline
- Shenandoah

---

## JVM

![](./hotspotjvm-1.PNG) <!-- .element: height="500" -->

--

### JVM Memory

![](./java-memory-model-3.png)

--

### Stack

![](./1200px-ProgramCallStack2_en.svg.png) <!-- .element: height="500" style="background: white" -->

--

```c [|8|9|2|10]
void func1(int z) {
  int x = 5; // allocate an integer on the stack in func1
  std::cout << "func1: x = " << x << std::endl;
  std::cout << "main: z = " << z << std::endl;
}

int main() {
  int z = 15; // allocate an integer on the stack in main
  func1(z); // call func1
  return 0; // after func1 ended, x is not longe allocated
}
```

--

### Stack Advantages

- Automatic deallocation
- No fragmantation
- Good cache utilization

--

### Heap

```c [|2|3|5|7]
int main() {
  int* ptr = new int; // allocate an integer on the heap
  *ptr = 5; // assign a value to the integer

  std::cout << "Value of ptr: " << *ptr << std::endl;

  delete ptr; // free the memory allocated on the heap

  return 0;
}
```

--

### Java Stack

per-thread stack frames:
- primitives data
- object references (pointers)

--

### Java Heap

- All objects

--

### Heap deallocation

How do you deal with deallocating memory on the heap?

---

## Memory management

--

### Manual

```c [7]
int main() {
  int* ptr = new int; // allocate an integer on the heap
  *ptr = 5; // assign a value to the integer

  std::cout << "Value of ptr: " << *ptr << std::endl;

  delete ptr; // free the memory allocated on the heap

  return 0;
}

--

### Reference counting

```c++ [|6]
int main() {
  std::shared_ptr<int> ptr1(new int(5)); // allocate an integer on the heap using a shared_ptr
  std::shared_ptr<int> ptr2 = ptr1; // create another shared_ptr that points to the same memory

  // decrement the reference count of the shared_ptr
  ptr1.reset();

  // decrement the reference count of the shared_ptr again
  ptr2.reset();

  return 0;
}
```

--

### Deferred reference counting

- Only count heap -> heap references
- Intermittedly scan for zero-ref objects

---

## Garbage collection

A process seperate from the mutator (application code) thats finds and removes **unreachable** objects

--

### In outline

- Mutator unchanged during normal operation
- Halted or changed while active

--

### Tracing garbage collection

<!-- .slide: class="fragmented-lists" -->
- Finds objects by tracing the references recursively from the root (stack)
  - Objects that **can't** be reached are considered dead / garbage
  - Objects that **can be** reached are marked live
- Sweep though memory and reclaim unmarked space
- Mark and Sweep

--

![](./mark.jpg)

--

### Serial & Parallel GC

![](./Stop-the-world-garbage-collection.jpg)

--

### Compaction

![](./GC-mark-sweep-compact.png)

--

### Generational GC

![](./Slide5.png)

--

### Remembered set

![](./fig1.jpg)

--

### G1GC

![](./g1gc.png)

--

![](./cycle.png)

--

### Shenandoah

```java
void example(Foo foo) {
  Bar b1 = foo.bar;             // Read
  while (..) {
    Baz baz = b1.baz;           // Read
    b1.x = makeSomeValue(baz);  // Write
}
```

--

### Shenandoah

```java
void example(Foo foo) {
  Bar b1 = readBarrier(foo).bar;             // Read
  while (..) {
    Baz baz = readBarrier(b1).baz;           // Read
    X value = makeSomeValue(baz);
    writeBarrier(b1).x = readBarrier(value); // Write
}
```