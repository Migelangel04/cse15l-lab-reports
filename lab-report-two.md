# Lab Report Two: Servers and Bugs

## Part One: StringServer

In this lab report, I utilized two files of code, one called "Server.java" and "StringServer.java".
Here is the code for Server.java:

```
import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;
import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }
}
```

In the Server.java file, I used the file given in Lab 2 to access the server and StringServer.java to start a new server on the local host (aka my machine). I attempted
to change the domain name of "localhost" to "stringserver" but after conducting research and experimenting, I realized the only way to change 
the server name is to change it using `sudo nano /etc/hosts` on the terminal and then changing the hostname to "stringserver". However, the terminals
at UCSD to do not give sudo commands to the students and modifying it on my machine would change my machine settings, so I stuck with localhost as the hostname.

From the knowledge provided in week 2 lectures, this code starts a basic web server using the local machine and then giving the user access to choose the port number.
The port number gives users a way to identify a specific process to which an internet or other network message is to be forwarded when it arrives at a server. This allows
StringServer.java to run:

```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler{

    String message = "";

    public String handleRequest(URI url)
    {
        
            if (url.getPath().contains("/add-message"))
            {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s"))
                {
                    
                    message += parameters[1] + "\n";
                    
                    return String.format(message, parameters[1], message);
                }
            }
        
        return "404 Not Found :("; 
    }

}


public class StringServer
{
    public static void main(String[] args) throws IOException{
        if (args.length == 0)
        {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }
        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```

StringServer.java has two tasks, retrieve the port number from the user and use the Handler class to output the string message to the web page. As we can see, StringServer has a main class which is charge of starting the local server with the designated port number. Starting the server is done using the terminal as shown:

![Image](https://migelangel04.github.io/cse15l-lab-reports/LabReport2(3).png)

Now that we have started the server, we can use either the `curl` function in the terminal or webpage search bar to change the contents on the webpage. For 
simplicity, we will modify the web page using the search bar. 

First Image:

![Image](https://migelangel04.github.io/cse15l-lab-reports/LabReport2(1).png)

In this first alteration of the webpage, I input `/add-message?s=Hello my name is Migelangel!` to the search bar after 'localhost:8000'. After the command is input, the handle request is sent to the Hanlder class which implements the URLHandler interface using the `handleRequest(URI url)` method. The `url` parameter contains the request input from the search bar. With this information, the StringServer.java file processes the URI. First, it is sent into the if statement to see if "/add-message" is contained within the URI and after grabs the query, `?`, and splits the contents after the query into an array. This is done in the "String[] parameter" line of the code. Then after the protacols are taken, the String `message` is altered with the intended string after the equals sign in the URI. The `message` is appended (not replaced) to the string along with the new line (\n) sequence. This process then outputs "Hello my name is Migelangel!" to the webpage.

Using similar methods, we obtain our second alteration:

![Image](https://migelangel04.github.io/cse15l-lab-reports/LabReport2(2).png)

Similar steps where taken as with the pervious method however, instead of the `message` string being completely replaced, we instead appended the new string input to our pervious input. This was accomplished by the `+=` operation for string addition and since we did not restart the server or use a different port, the values of Image One were saved.

## Part Two

For this part of the Lab Report, I will be referring to the files ArrayExamples.java and ArrayTest.java from Lab 3. In particular, the bug that I have choosen to discuss is the method `reverseInPlace(int[] arr)` in ArrayExamples.java. 

Here is the Original code for the ArrayExamples.java:

```
public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }


}
```

This is the code we started with in Lab 3 and here is the Testing and results for this particular method:

Code (One Non-failure Inducing Input and Two Failure Inducing):

```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {

  @Test 
  //Sucessful Testing
  public void testReverseInPlace1()
  {
    int[] input = {};
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(new int[]{}, input);
  }

  @Test 
  //Failure Inducing
  public void testReverseInPlace2()
  {
    int[] input1 = {1, 2, 3, 4, 5, 6};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{6, 5, 4, 3, 2, 1}, input1);
  }

  @Test
  //Failure Inducing
  public void testReverseInPlace3()
  {
    int[] input1 = {1, 2, 3, 4, 5, 6, 7};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{7, 6, 5, 4, 3, 2, 1}, input1);
  }

}
```

JUnit Terminal testing:

![Image](https://migelangel04.github.io/cse15l-lab-reports/LabReport2(6).png)

As we can see, I ran three test for this method; testReversedInPlace1(), testReversedInPlace2(), and testReversedInPlace3(). In the first test I passed in an empty `int` array and it returned with a sucessful test, meaning an input that did not induce a failure symptom. 

However, with the other two tests, there were noticeable failure symptoms. In testReversedInPlace2, I passed in an array of length 6 starting at one and ending at six and expected the values to be in reverse order (i.e. 6, 5, 4, 3, 2, 1) however in the JUnit test, the element at element 3 was suppose to be 3 but instead was 4. Moreover, in testReversedInPlace3 the same issue occurred but in this case, the lenth of the array is 7 and the element of error was 4. 

Notice how the error happens after the midpoint of the array for an odd length array and at the midpoint for an array of even length (excluding length 0 and 1).

This is the method that caused the error:

```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

This would be a potiential solution:

```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2 ; i += 1) {
      int dummyOne = arr[i];
      int dummyTwo = arr[arr.length - i - 1];
      arr[i] = dummyTwo;
      arr[arr.length - i - 1] = dummyOne;
    }
  }
  
```

The two major changes made was `arr.length / 2` in the conditional statement of the for loop and the addition of dummy variables in the for loop body. These dummy variables were made to save the values at each end of the array and then transfer them once they were both saved. This makes sure that when coping the values to either side, we keep the values instead of losing them like the pervious code block. Moreover, the conditon change assured we do not copy the newly changed values back to the 2nd half of the array. This takes advantage of integer divison. 

## Part Three

Two interesting things I learned in lab was starting a server using basic lines of java code and the use of JUnit using the terminal on VSCode. I never knew that the backend of webpages worked similar to the code presented in Lab 2 (of course at a much more complicated degree) and it really sparked my interest in learning more about backend web development. Moreover, the use of VSCode and JUnit is very useful, especially in CSE12, because it allows me to get more comfortable with the terminal and gives me a way to use JUnit testing without having to use Eclipse all the time. 






