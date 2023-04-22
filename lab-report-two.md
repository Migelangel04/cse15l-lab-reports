# Lab Report Two: Servers and Bugs

## Part One: StringServer

In this lab report, I made two files of code, one called "Server.java" and "StringServer.java".
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

In the Server.java file, I used the file given in Lab 2 to access the server and StringServer.java and start a new server on the local host. I attempted
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

What StringServer.java does is 




