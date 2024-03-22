# Commit 1 Reflection
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