Functional Interface
Any interface with a single abstract method is a functional interface.

Method Reference
Java provides a new feature called method reference in Java 8. Method reference is used to refer method of functional interface. It is compact and easy form of lambda expression. Each time when you are using lambda expression to just referring a method, you can replace your lambda expression with method reference.

Types of Method References
Reference to a static method
interface Sayable{  
    void say();  
}  
public class MethodReference {  
    public static void saySomething(){  
        System.out.println("Hello, this is static method.");  
    }  
    public static void main(String[] args) {  
        // Referring static method  
        Sayable sayable = MethodReference::saySomething;  
        // Calling interface method  
        sayable.say();  
    }  
}  

Reference to an instance method
interface Sayable{  
    void say();  
}  
public class InstanceMethodReference {  
    public void saySomething(){  
        System.out.println("Hello, this is non-static method.");  
    }  
    public static void main(String[] args) {  
        InstanceMethodReference methodReference = new InstanceMethodReference(); // Creating object  
        // Referring non-static method using reference  
            Sayable sayable = methodReference::saySomething;  
        // Calling interface method  
            sayable.say();  
            // Referring non-static method using anonymous object  
            Sayable sayable2 = new InstanceMethodReference()::saySomething; // You can use anonymous object also  
            // Calling interface method  
            sayable2.say();  
    }  
}
Reference to a constructor
interface Messageable{  
    Message getMessage(String msg);  
}  
class Message{  
    Message(String msg){  
        System.out.print(msg);  
    }  
}  
public class ConstructorReference {  
    public static void main(String[] args) {  
        Messageable hello = Message::new;  
        hello.getMessage("Hello");  
    }  
} 

Predicate
The Predicate functional interface is a specialization of a Function that receives a generified value and returns a boolean.

List<String> names = Arrays.asList("Angela", "Aaron", "Bob", "Claire", "David");
List<String> namesWithA = names.stream()
  .filter(name -> name.startsWith("A"))
  .collect(Collectors.toList());
Consumer
The Consumer functional interface accepts a generified argument and returns nothing.

List<String> names = Arrays.asList("John", "Freddy", "Samuel");
names.forEach(name -> System.out.println("Hello, " + name));
BiPredicate
BiPredicate accepts two argument and returns Boolean value. Apply business logic for the values passed as an argument and return the boolean value. BiPredicate functional method is test(Object, Object).

BiPredicate <Integer, Integer> biPre = (a,b) -> a==b;
System.out.println(biPre.test(5,10));
System.out.println(biPre.test(10,10));
BiConsumer
BiConsumer does not return value. It accepts two parameter as an argument. BiConsumer functional method is accept(Object, Object). This methods performs the operation defined by BiConsumer.

BiConsumer<String, Integer> biCon = (a,b) -> System.out.println(a+” “+b);
biCon.accept(“A”, 10);
biCon.accept(“B”, 20);
Predicate inside a method
class PredicateInterfaceExample3 { 
    static void pred(int number, Predicate<Integer> predicate) { 
        if (predicate.test(number)) { 
            System.out.println("Number " + number); 
        } 
    } 
    public static void main(String[] args) { 
        pred(10, (i) -> i > 7); 
    } 
} 
Implement two predicates
public class PredicateInterfaceExample2 { 
    public static void main(String[] args) 
    { 
        Predicate<Integer> greaterThanTen = (i) -> i > 10; 
  
        // Creating predicate 
        Predicate<Integer> lowerThanTwenty = (i) -> i < 20;  
        boolean result = greaterThanTen.and(lowerThanTwenty).test(15); 
        System.out.println(result); 
  
        // Calling Predicate method 
        boolean result2 = greaterThanTen.and(lowerThanTwenty).negate().test(15); 
        System.out.println(result2); 
    } 
}
Predicate and
class PredicateInterfaceExample5 { 
    public static Predicate<String> hasLengthOf10 = new Predicate<String>() { 
        @Override
        public boolean test(String t) { 
            return t.length() > 10; 
        } 
    }; 
  
    public static void predicate_and() { 
        Predicate<String> nonNullPredicate = Objects::nonNull; 
  
        String nullString = null; 
  
        boolean outcome = nonNullPredicate.and(hasLengthOf10).test(nullString); 
        System.out.println(outcome); 
  
        String lengthGTThan10 = "Welcome to the machine"; 
        boolean outcome2 = nonNullPredicate.and(hasLengthOf10). 
        test(lengthGTThan10); 
        System.out.println(outcome2); 
    } 
    public static void main(String[] args) { 
        predicate_and(); 
    } 
} 


Predicate or
class PredicateInterfaceExample4 { 
    public static Predicate<String> hasLengthOf10 = new Predicate<String>() { 
        public boolean test(String t) { 
            return t.length() > 10; 
        } 
    }; 
  
    public static void predicate_or() { 
  
        Predicate<String> containsLetterA = p -> p.contains("A"); 
        String containsA = "And"; 
        boolean outcome = hasLengthOf10.or(containsLetterA).test(containsA); 
        System.out.println(outcome); 
    } 
    public static void main(String[] args) { 
        predicate_or(); 
    } 
} 
Supplier
Supplier represents a function which does not take in any argument but produces a value of type T.
Function
The most simple and general case of a lambda is a functional interface with a method that receives one value and returns another.
BiFunction
BiFunction represents a function which takes in two arguments and produces a result.
Optional
The purpose of the Optional class is to provide a type-level solution for representing optional values instead of null references.

To create an empty Optional object, we simply need to use its empty static method:
Optional<String> empty = Optional.empty();

We can also create an Optional object with the static method of:
Optional<String> opt = Optional.of(name);

But, in case we expect some null values, we can use the ofNullable() method:
String name = "baeldung";
Optional<String> opt = Optional.ofNullable(name);

Checking Value Presence: isPresent() and isEmpty()
Conditional Action With ifPresent()
Stream
A stream is a sequence of objects that supports various methods which can be pipelined to produce the desired result.
Intermediate Operations:

map: The map method is used to map the items in the collection to other objects according to the Function passed as argument.

List number = Arrays.asList(2,3,4,5);
List square = number.stream().map(x->x*x).collect(Collectors.toList());

filter: The filter method is used to select elements as per the Predicate passed as argument.

List names = Arrays.asList("Reflection","Collection","Stream");
List result = names.stream().filter(s->s.startsWith("S")).collect(Collectors.toList());

sorted: The sorted method is used to sort the stream.
List names = Arrays.asList("Reflection","Collection","Stream");
List result = names.stream().sorted().collect(Collectors.toList());
Terminal Operations:

collect: The collect method is used to return the result of the intermediate operations performed on the stream.
List number = Arrays.asList(2,3,4,5,3);
Set square = number.stream().map(x->x*x).collect(Collectors.toSet());

forEach: The forEach method is used to iterate through every element of the stream.
List number = Arrays.asList(2,3,4,5);
number.stream().map(x->x*x).forEach(y->System.out.println(y));

reduce: The reduce method is used to reduce the elements of a stream to a single value.
The reduce method takes a BinaryOperator as a parameter.
List number = Arrays.asList(2,3,4,5);
int even = number.stream().filter(x->x%2==0).reduce(0,(ans,i)-> ans+i);
Peek
Stream peek(Consumer action) returns a stream consisting of the elements of this stream, additionally performing the provided action on each element as elements are consumed from the resulting stream. This is an intermediate operation i.e, it creates a new stream that, when traversed, contains the elements of the initial stream that match the given predicate.
anyMatch, allMatch, noneMatch
Stream.anyMatch() returns whether any elements of this stream match the provided predicate. May not evaluate the predicate on all elements if not necessary for determining the result. If the stream is empty then false is returned and the predicate is not evaluated.

Stream.allMatch() returns whether all elements of this stream match the provided predicate. May not evaluate the predicate on all elements if not necessary for determining the result.

Stream.noneMatch() returns whether no elements of this stream match the provided predicate.
findFirst, findAny
findAny() method allows you to find any element from a Stream.

The findFirst() method finds the first element in a Stream.
Stream.generate()
Stream generate(Supplier<T> s) returns an infinite sequential unordered stream where each element is generated by the provided Supplier. This is suitable for generating constant streams, streams of random elements, etc.
Autoboxing, unboxing
Autoboxing: Converting a primitive value into an object of the corresponding wrapper class is called autoboxing. For example, converting int to Integer class. 

Unboxing: Converting an object of a wrapper type to its corresponding primitive value is called unboxing. For example conversion of Integer to int.
IntSteam.range()
IntStream range(int startInclusive, int endExclusive) returns a sequential ordered IntStream from startInclusive (inclusive) to endExclusive (exclusive) by an incremental step of 1.

Example:
class GFG { 
    public static void main(String[] args) { 
        IntStream stream = IntStream.range(6, 10); 
        stream.forEach(System.out::println); 
    } 
}

Output:
6
7
8
9
IntSteam.rangeClosed()
IntStream rangeClosed(int startInclusive, int endInclusive) returns an IntStream from startInclusive (inclusive) to endInclusive (inclusive) by an incremental step of 1.

Example:
class GFG { 
    public static void main(String[] args) { 
        IntStream stream = IntStream.rangeClosed(-4, 3);
        stream.forEach(System.out::println); 
    } 
}

Output:
-4
-3
-2
-1
0
1
2
3
Aggregate function - sum(), max(), min(), average()
Example:
IntStream stream = IntStream.of(2, 4, 6, 1, 34, 5, 9);
int max = stream.max().getAsInt(); // max() returns OptionalInt

stream = IntStream.of(2, 4, 6, 1, 34, 5, 9);
int min = stream.min().getAsInt(); // min() returns OptionalInt

stream = IntStream.of(2, 4, 6, 1, 34, 5, 9);
double average = stream.average().getAsDouble(); // average() returns OptionalDouble

stream = IntStream.of(2, 4, 6, 1, 34, 5, 9);
int sum = stream.sum(); // sum() returns int

System.out.println("max : " + max);
System.out.println("min : " + min);
System.out.println("average : " + average);
System.out.println("sum : " + sum);

Output:
max : 34
min : 1
average : 8.714285714285714
sum : 61

