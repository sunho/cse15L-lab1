# Part 1

## Code

```java
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.lang.RuntimeException;

class Handler implements URLHandler {
  ArrayList<String> words = new ArrayList<String>();

  public String handleRequest(URI url) {
    try {
      if (url.getPath().startsWith("/add-message")) {
        if (!url.getQuery().startsWith("s=")) {
          throw new RuntimeException("No word was specified in query");
        }
        String word = url.getQuery().substring(2);
        words.add(word);
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < words.size(); i++) {
          sb.append(String.format("%d. %s\n", i+1, words.get(i)));
        }
        return sb.toString();
      }
      return "404 Not Found!";
    } catch(RuntimeException e) {
      return String.format("500 Runtime Error: %s", e.toString());
    }
  }
}

class StringServer {
  public static void main(String[] args) throws IOException {
    if(args.length == 0){
      System.out.println("Missing port number! Try any number between 1024 to 49151");
      return;
    }

    int port = Integer.parseInt(args[0]);

    Server.start(port, new Handler());
  }
}
```

## First command

![fa](/images/server1.png)

**Which methods in your code are called?**

handleRequest is getting called.

**What are the relevant arguments to those methods, and the values of any relevant fields of the class?**

URL is the relevant argument and that class have fields query, path, etc. words field of the class is also relevant. It contains no element yet.

**How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.**

words array list get added "Hello" string.


## Second command

![fa](/images/server2.png)

**Which methods in your code are called?**

handleRequest is getting called.

**What are the relevant arguments to those methods, and the values of any relevant fields of the class?**

URL is the relevant argument and that class have fields query, path, etc. words field of the class is also relevant. It contains one entry "Hello".

**How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.**

words array list get added "How are you" string.

# Part 2

## The path to the private key for your SSH key

![fa](/images/ssh1.png)

I already use id_rsa for something else so id_rsa_uscd is the one for ucsd server.

## The path to the public key for your SSH key

![fa](/images/ssh2.png)

## A terminal interaction where you log into ieng6 with your course-specific account without being asked for a password.

![fa](/images/ssh3.png)

# Part 3

I learned that ucsd has free linux server. I also learned about some history of linux commands.
