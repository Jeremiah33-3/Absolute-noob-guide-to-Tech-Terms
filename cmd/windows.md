## Quick syntax

### Multiple lines
Use backticks (\`) for line breaks. Add `;` after each line
E.g.:
```linux
curl -o example.zip https://files.example.io/example.zip;
tar -xf example.zip;
cd competition_package
```

### Facts about `curl` on Windows

In PowerShell, the command `curl` is actually an alias for a native Windows command called `Invoke-WebRequest`. It is not the actual tool "cURL" that the rest of the world uses.

The Bottleneck: `Invoke-WebRequest` is famously slow for large file downloads because it tries to parse the response stream and update a complex progress bar (the "Writing web request" status you see) which consumes massive amounts of CPU and memory, effectively throttling your download speed.

The Solution: By typing `curl.exe` explicitly, you tell PowerShell to ignore its internal alias and use the actual Curl program installed on Windows, which is fast and efficient.

E.g.
```linux
curl.exe -o starterpack.zip https://files.example.com/starterpack.zip
```
