# The HTTP Request Lifecycle

## Step 1: Lcoal Processing

- Browswer extracts the "schema"/protocol (host www.example.com) and optional port number, resource path, and the query strings that are specified in the form.

 ```
 <protocol>://<host><:optional port>/<path/to/resource><?query>. An example is |http|://|www.example.com||:5000||/mainpage||?query=param&query2=param2|
 ```

- browser now has the intended hostname for the request, it needs to resolve an IP address.
- first, the brower will look through it's own cache of recently requested URL's, the OS's cache of recent queries, your router's cache and your DNS cache.

## Step 2: Resolve an IP

- If cache lookup fails, your browser fires of a DNS request using UDP. The DNS request contians the preconfig IP for your DNS server and your return IP in its header.
- The hostname for which you are tyring to resolve an IPS is in the request's  "Question" section.
- request travels through many network devices to reach its target DNS server. 
- Once your request arrive at your config DNS server, the server looks for the address associated with the requested hostman.
- If finds one, it send a response. If not, passes the request along to another DNS server it is config to defer to. 
- This happens recursively until the address is found, or an "authoritative" nameserver is hit.
- Once the request is successfully through, the client now has target IP and will also recieve a peice of information as part of the answer that will let it know how long the returned answer can be cached for.

## Step 3: Establish a TCP Connection

- Now that the client has an IP address, it can send an HTTP request once it open a TCP connection (transport layer protocol, like UDP).
- TCP vs UDP - TCP ensures delivery adn orderd data tranmission. Done very simply using sequence numbe rof every byte sent. This allows the reciever to re-orer recieved pacekts bakc into their original order, also allows sender to retransmit any packet that does not get recognized by the receiver.
- TCP connnections are opened using the three-way handshake. The server mush alreayd be "listening" on port , performing a passive open, after which the client can inititate an active open.
  - client initiatate the active open by sending a `SYN` control packedt to the server
  - server responsds with a `SYN-ACK` message, which contains an acknowledgement nubmer for the original message taht is alway `x+1` and a new sequence nubmer for teh response itself (another random number `y`)
  - client then sends a `ACK` message back to the server with a sequence nubmer eqaul to `x+1`, which should match the `SYN-ACK` message's acknowledgement number and ensure that our data is being delivered realiably.

## Step 4: Send an HTTP Request

- Now the client has an IP address and a TCP connnection, it can finally send an HTTP request.
- request is made up of a "request line", request header and a body. The request line is a line that indicates the HTTP method, the resource being requested , and the protocol version.
- The header is made up of pari in the form `name:value <CR><LF>`
- The only mandatory field in an HTTP request is `HOST`, which contains the domain and prot that the request is beign sent to.
- Once the HTTP reaquest is sent, it follows similar routing procedures as the one discussed earlier, with the difference being that usign TCPs magic sequence number power, the serve can ensure it receives the whole request, in the correct order.
- server recieves the request, processes it, and finds the resource being requested, it generates an HTTP response (similar structure to an HTTP request)
- Once the response is generated, the server responds to the request. At the TCP layer the client receives teh frist data packet, the first byte of which should contain the HTTP response header. Packets continue to come in, and at the TCP layer they are re-ordered as needed.

## Step 5: Tearing Down and Cleaning up

- once the response has been fully delievered, the client sends a `FIN` packet at the TCP level, to which the server responds with an `ACK` and then generally send a `FIN` of its own and cient responds with its own `ACK` siganl.
- Client then waits briefly and cannnot accept new connections to prevent delayed packets from pervious connenctions arriving during subsequest activities on the port.
- This four-way handshake signals the end of the TCP connection.
- Broswer begins to process what is has recieved (image, data, media files) by some application insdie the broswer.
- HTML gets parsed, processes links and spins up new requests for that content if needed, restarting the whole cycle.

## Do a Simple HTTP Request in Java

### HTTpURLConnection

- performs basic HTTP requests without the use of any additional libraries.
- all classes needed are part of the `java.net` package.
- code can be more cumbersome than other HTTP libraries and doesn't provide more advanced functionalities such as dedicated methods for adding headers or auth.

### Creating a Request

- create using openConnection() method of the URL class.
- this method only created a connection object but does not establish the connection yet.

```
URL url = new URL("http://example.com");
HttpURLConnection con = (HttpURLConnection) url.openConnection();
con.setRequestMethod("GET"
```

### Adding Request Parameters

- you need the `doOutput` property to true, then write a String of the form `param1=value¶m2=value` to the OutputStream of the HttpUrlConnection instance:

```
Map<String, String> parameters = new HashMap<>();
parameters.put("param1", "val");

con.setDoOutput(true);
DataOutputStream out = new DataOutputStream(con.getOutputStream());
out.writeBytes(ParameterStringBuilder.getParamsString(parameters));
out.flush();
out.close();
```

### Setting Request Headers

- adding headers to a request can be achieved by using the `setRequestProperty()` method.

```
con.setRequestProperty("Content-Type", "application/json");

// read the value of a header
String contentType = con.getHeaderField("Content-Type");
```

### Configuring Timeouts

- HTTPUrlConnnect class allows setting the connenct and read timeouts. These values define the interval of time to wait for the connenciton to the server to be established or data to be available for reading.

```
con.setConnectTimeout(5000);
con.setReadTimeout(5000);
```

### Handling Cookies

- To read the cookies from a response, retrieve the value of the Set-Cookie header and parse it to a list of HTTPCookie objects;

```
String cookiesHeader = con.getHeaderField("Set-Cookie");
List<HttpCookie> cookies = HttpCookie.parse(cookiesHeader);

// map through the cookies
cookies.forEach(cookie -> cookieManager.getCookieStore().add(null, cookie));

// check cookies for username
Optional<HttpCookie> usernameCookie = cookies.stream()
  .findAny().filter(cookie -> cookie.getName().equals("username"));
if (usernameCookie == null) {
    cookieManager.getCookieStore().add(null, new HttpCookie("username", "john"));
}

// add cookies to the request
con.disconnect();
con = (HttpURLConnection) url.openConnection();

con.setRequestProperty("Cookie", 
  StringUtils.join(cookieManager.getCookieStore().getCookies(), ";"));
```

### Handling Redirects

- enable or disable auto following redirects for a specific connection

```
con.setInstanceFollowRedirects(false);

// disable/enable auto redirect for all connenctions
HttpUrlConnection.setFollowRedirects(false);
```

### Reading the Response

- parsing the InputStream of the HTTPUrlConnection instance. Use getResponseCode(), connect(), getInputStream() or getOutputStream() methods.

```
int status = con.getResponseCode();

// read the response of request and place it in a content string

BufferedReader in = new BufferedReader(
  new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer content = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    content.append(inputLine);
}
in.close();

```

### Reading the Response on Failed Requests

- if request fails trying to read InputStream, consume the stream provided by HTTPUrlConnnection.getErrorStream()

```
int status = con.getResponseCode();

Reader streamReader = null;

if (status > 299) {
    streamReader = new InputStreamReader(con.getErrorStream());
} else {
    streamReader = new InputStreamReader(con.getInputStream());
}

```

### Building the Full Response

- build using the method from HTTPUrlConnection instance offers:

```
public class FullResponseBuilder {
    public static String getFullResponse(HttpURLConnection con) throws IOException {
        StringBuilder fullResponseBuilder = new StringBuilder();

        // read status and message

        // read headers

        // read response content

        return fullResponseBuilder.toString();
    }
}
```

#### Add the response status information

```
fullResponseBuilder.append(con.getResponseCode())
  .append(" ")
  .append(con.getResponseMessage())
  .append("\n");
```

#### Get headers using the getHeaderFields()

- add each of them to our StrigBuilder in the format HeaderName: HeaderValues

```
con.getHeaderFields().entrySet().stream()
  .filter(entry -> entry.getKey() != null)
  .forEach(entry -> {
      fullResponseBuilder.append(entry.getKey()).append(": ");
      List headerValues = entry.getValue();
      Iterator it = headerValues.iterator();
      if (it.hasNext()) {
          fullResponseBuilder.append(it.next());
          while (it.hasNext()) {
              fullResponseBuilder.append(", ").append(it.next());
          }
      }
      fullResponseBuilder.append("\n");
});
```

## Sources

[Daniel Golant](https://dev.to/dangolant/things-i-brushed-up-on-this-week-the-http-request-lifecycle-)
[Baeldung](https://www.baeldung.com/java-http-request)
