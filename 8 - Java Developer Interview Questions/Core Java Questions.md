 1. What are Functional Interfaces and why are they important?
 2. Mention some commonly used predefined functional interfaces in Java.
 3. What is the Stream API and how does it improve performance?
 4. Write a Stream program to find the square of all odd numbers in a list.
 5. Write a simple Java program to check if a string is palindrome or not.
 6. What do you mean by Multithreading in Java?
 7. Different ways to create threads in Java.
 8. Explain the concept of Java Memory Model (JMM).
 9. Difference between volatile and synchronized keywords.
 10. Limitations or drawbacks of using the synchronized keyword.
 11. Streams, Multithreading, Exception Handling,
 1. What are the benefits of sealed classes introduced in Java 17? 
2. How do virtual threads in Java 21 improve request handling in high-load systems? 
3. What is the difference between Optional.map() and Optional.flatMap()? 
4. How does garbage collection differ in Serial, Parallel, and G1 collectors? 
5. How does var help with type inference in Java? 
6. Explain the difference between CopyOnWriteArrayList and ArrayList. 
7. What is the purpose of CompletableFuture in asynchronous programming? 
8. How does pattern matching for switch improve readability in Java 17+? 
9. What are text blocks, and how do they simplify working with JSON/XML? 
10. Explain immutability and how to enforce it in Java.  

---

```java
import java.io.*;
import java.util.*;

public class Example {

    public static void main(String[] args) throws IOException {
        System.out.println("Code started");

        // BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        // String name = br.readLine() ;
        // int year_of_birth = Integer.parseInt(br.readLine());

        // Or

        Scanner sc = new Scanner(System.in);
        String name = sc.nextLine();
        int year_of_birth = sc.nextInt();

        System.out.println("Hi " + name + " your year_of_birth is " + year_of_birth);
        System.out.println("Hello code run sucessfully");
        sc.close();
    }
}
```