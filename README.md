# Commit 1 Reflection notes
import 
```rust
std::io::prelude::*;
std::io::BufReader;
```
for 
```rust
let buf_reader = BufReader::new(&mut stream);
```

To handle the connection

```rust
let http_request: Vec<_> = buf_reader
        .lines()
        .map(|result| result.unwrap())
        .take_while(|line| !line.is_empty())
        .collect();
```

```.lines()``` is for seperating data stream each occurences. \
 ```.map``` is for unwraping each result to String. \
 ```.take_while(|line| !line.is_empty())``` do while loop untul found empty line and then loop breaks. \
 ```collect()``` is for combining the result into a vector.

# Commit 2 Reflection notes
```rust
let status_line = "HTTP/1.1 200 OK";
let contents = fs::read_to_string("hello.html").unwrap(); 
let length = contents.len();
let response = format!("{status_line}\r\nContent-Length: 
{length}\r\n\r\n{contents}");
stream.write(response.as_bytes()).unwrap();
```
```let status_line = "HTTP/1.1 200 OK";``` is for setting the status line. \
```fs::read_to_string("hello.html").unwrap();``` is for reading the file and unwraping it to String. \
```contents.len();``` is for getting the length of the file. \
```format!("{status_line}\r\nContent-Length: {length}\r\n\r\n{contents}");``` is for formating the response. \
```stream.write(response.as_bytes()).unwrap();``` is for writing the response to the stream.

![alt text](/assets/images/image.png)

# Commit 3 Reflection notes
```rust
let http_request= buf_reader.lines().next().unwrap().unwrap();
let (status_line, filename) = if http_request == "GET / HTTP/1.1" {
("HTTP/1.1 200 OK", "hello.html")
} else {
("HTTP/1.1 404 NOT FOUND", "404.html")
};
```
```let http_request= buf_reader.lines().next().unwrap().unwrap();``` is for getting the first line of the request. \
```let (status_line, filename) = if http_request == "GET / HTTP/1.1" {("HTTP/1.1 200 OK", "hello.html")} else {("HTTP/1.1 404 NOT FOUND", "404.html")};``` is for checking the request and setting the status line and filename.
![alt text](/assets/images/image2.png)

# Commit 4 Reflection notes
```rust
let (status_line, filename) = match &http_request[..] {
        "GET / HTTP/1.1" => ("HTTP/1.1 200 OK", "hello.html"), "GET /sleep HTTP/1.1" => {
        thread::sleep(Duration::from_secs(10)); ("HTTP/1.1 200 OK", "hello.html") }
        _ => ("HTTP/1.1 404 NOT FOUND", "404.html"),
};
```
```let (status_line, filename) = match &http_request[..] { "GET / HTTP/1.1" => ("HTTP/1.1 200 OK", "hello.html"), "GET /sleep HTTP/1.1" => { thread::sleep(Duration::from_secs(10)); ("HTTP/1.1 200 OK", "hello.html") } _ => ("HTTP/1.1 404 NOT FOUND", "404.html"),};``` is for checking the request and setting the status line and filename. \
```thread::sleep(Duration::from_secs(10));``` is for making the thread sleep for 10 seconds.