
## Introduction

Distributed systems connect different network computers by passing messages and coordinating between them. In concurrent systems many computers run commands inside the network. Concurrency means that several programs are running at the same time with eachother. There is no global clock for the distibuted systems so keeping the programs syncronized is an important aspect of maintaining correct running of distributed systems. Failures can and will happen within the network. Because the programs are no longer running in single threaded systems, there will be a series of new challenges in imlementing the DS. Diffent models can be used to overcome these challenges and having standardized models help to limit faults and readability and maintainablity of the codebase. 

**Network** is a collection of entities that can execute different software.

**Node** A node is the name for each entity that exist within the network. 

**Communication** is the interaction between each of the Nodes in the Network 

**Architecture models** These are models that allow abstractions and patterns for entities and communication in the network. 

**Message Passing** Nodes that send information from one node to another 

**Shared Memory** Nodes communicate through some shared memory storage example a database, where each of the nodes can read and write to/from. 

**Client-Server Architecture** Are different nodes that communicate through message-passing (Invocations) in conjunction with a Server. Here the nodes send some request for the server to handle some complex actions and then send back the results

**Peer-to-Peer** networks where nodes are interconnected with serveres

Having more servers can increase resilience against failures. 

## Lecture 2 

**Pointers**

Pointers in Go work in a similar way to references in languages like Java. In memory each entry has an address, a type and a value. With pointers you can reference the address of a variable this can be done using the '&' sign 

```go 
var myVar int myVar = 5 
var myPointer 
*int myPointer = &myVar 
```

in this way the actual address of the variable is stored this allows one to write more precise code. 

**Slices**

Slices are dynamic arrays they are are data structures which have a length a capacity and a pointer to the head of the array.  You can expand the slices because you do not need to reallocate memory if you are within the size of the array. 

Remember to use make and append when using slices. 

```go
var mySlice = []int 
mySlice = []int{1,2,3,4,5,6,7} // static array is a slice with the declared size and capacity of the array

// with allocation 
var numbers = make(int[]{2,2}) // int, length 2, capacity 2
numbers[3] = 3 // error assign to nonexistant 3rd element OOB

fmt.Println(append(mySlice, 3)) // 
```


**Go functions**
Use functions when possible they work similar to java methods without the Object-Oriented boiler plate. 

``` go 
func transpose(a [][] string) [][]string { // return values are written last
	// some function
}
```


**Call by value and call by reference** with call by value you pass the some value to the function as an input value. But you can also call by reference by passing the reference or the pointer/address to the method. 

### Threads and Synchronization 

Distributed systems run **concurrently** meaning that the programs can run side-by-side. So you can have many sequences of programs that run in parallel, while accessing the same part of memory. 

**Threads**
Programs can spawn many threads (or cores, which are galled goroutines in Go). Threads execute in parallel they can access memory and resources. There is a danger that without proper synchronization the results can be unstructured. 

"Threads are parallel execution of code within the same process." Threads within the same process share the same memory. 

``` go 
f() // call f() wait for it to return 

go f() // create a new goroutine that calls f(); don't wait

//spinner example 
go spinner() // prints spinning 

fibN := fib(n)
fmt.Printf("\rFibonacci(%d) = %d", n, fibN)
```

When the main program breaks or is done running all the threads that are children of that routine will also stop. Running things in parallel, may, make things faster, but the action of spinning up threads also takes resources so its mostly applicable for larger applications. 

  
**Race Condition**
Situations in which a program does not give the correct result for some interleaving of the operations of multiple goroutines (threads. ) When multiple threads access the same variable at the same time Race conditions occur.  
These errors are hard to reproduce and diagnose. This is important in things like databases, where you need to make sure that parallel reads and writes to the database return the expected results. 

you can lock variables with the sync.Mutex  this way you can help ensure the stability of the program. 

```go
var arbiter sync.Mutex

func worker() {
	arbiter.Lock()
	balance++
	arbiter.Unlock()
}

```

Error can occur because if multiple threads read some variable, save it and then increment it then reassign it to memory. So while the computation of for example incrementing, the other thread is doing the same increment operation leading to unexpected results. Race condition is happening because the threads are in a race to get access to the resources. 

**Channels**

Data structure that can be used by threads to communicate. Channels are queues for threads to read and write to

```go
ch := make(chan int) // ch has type 'chan int' 
ch <- x  // a send statement 
x = <-ch // a receive expression in an assignment statement 
<-ch     // a receive statement; result is discarded


// channels can be synchronous or asynchrounous 

// channels can be made into buffers 
ch := make(chan int, 4) // buffer of size 4 

```

with buffers you can use the buffer space, but if it is full then the channel will be blocked for acces by other threads. 