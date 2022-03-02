# Java Primitives versus Objects

- Java has a two-fold type system consisting of primitives such an `int`, `boolean` and reference types such as `Interger`, `Boolean`.
- every primitive type corresponds to a reference type.
- every object contains a single value of the corresponding primitive type.
- The wrapper classes are immutable(state cannot change once the object is constructed) and are final.
- Java performs a conversion between the primitvie and reference types if an actual type is different from the declared one:
    - `Interger j = 1;`
    - `int i = new Interger();`
- this conversion is called autoboxing.

## Single Item Memory Footprint

- `boolean` - 1bit
- `byte` - 8 bits
- `short,char`- 16bits
- `int, float` - 32bits
- `long, double` - 64bits

- primitive types live in the stack and are able to be accessed quite fast.
- reference types live on the heap and are relatively slow to access.
- `Boolean` - 128bits
- `Byte` - 128bits
- `Short, Character` - 128bits
- `Interger, Float` - 128bits
- `Long, Double` - 128bits

## What is an Exception

- an exception is an event, which occurs during the execution of a program, that disrupts the normal flow of the program's instructions.
- when an error occurs within a method, the method created an object and hands it off to the runtime systme.
- the excetion object contians information about the error (type, state of the program when it occurred,etc)
- creating an exception object and handling it to the runtime system is called `throwing an exception`
- after the exception, the RTS attempts to find something to handle it.
- the RTS searches the call stack for a method that contains the block of code that can hangle the exception, called the exception handler.

## Catching and Handling exceptions

```
// Note: This class will not compile yet.
import java.io.*;
import java.util.List;
import java.util.ArrayList;

public class ListOfNumbers {

    private List<Integer> list;
    private static final int SIZE = 10;

    public ListOfNumbers () {
        list = new ArrayList<Integer>(SIZE);
        for (int i = 0; i < SIZE; i++) {
            list.add(new Integer(i));
        }
    }

    public void writeList() {
	// The FileWriter constructor throws IOException, which must be caught.
        PrintWriter out = new PrintWriter(new FileWriter("OutFile.txt"));

        for (int i = 0; i < SIZE; i++) {
            // The get(int) method throws IndexOutOfBoundsException, which must be caught.
            out.println("Value at: " + i + " = " + list.get(i));
        }
        out.close();
    }
}
```
- the constructor initializes an output stream on a file and if the file cannot be opened, the constructor throws an `IOException`.
- The `IndexOutOfBoundsException` is thrown if the argument is too small or too larger (larger than the array elements in the list).
- `IOException` is a checked exception (thrown by the constructor)
- `IndexOutOfBoundsException` is an unchecked exception and its thrown by the `get()` method.

## Scanning

- objects of type `Scanner` are useful for breaking down formatted input into tokens and translating individual token according to their data type.

```
import java.io.*;
import java.util.Scanner;

public class ScanXan {
    public static void main(String[] args) throws IOException {

        Scanner s = null;

        try {
            s = new Scanner(new BufferedReader(new FileReader("xanadu.txt")));

            while (s.hasNext()) {
                System.out.println(s.next());
            }
        } finally {
            if (s != null) {
                s.close();
            }
        }
    }
}
```
- need to close the `Scanner` object to indicate you're done with its underlying stream.
- `Scanner` supports tokens for all of the Java primitives types (except for char) as well as `BigInterger` and `BigDecimal`.


### Sources

[Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/handling.html)  
[Primitives versus Objects](https://www.baeldung.com/java-primitives-vs-objects)  
[Scanner](https://docs.oracle.com/javase/tutorial/essential/io/scanning.html)  
