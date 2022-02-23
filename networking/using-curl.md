# Using Curl

> Resources:
> - https://flaviocopes.com/http-curl/

Curl is a command line tool that lets you make network requests.
It is extremely valuable when debugging various network protocols such as HTTP, HTTPS, FTP, SFTP, SMTP, etc.

It has been described as 
> A programmer's best friend

### HTTP GET Request

```bash
curl <url>
```
### Get HTTP Respose Headers

```bash
curl -i <url>
```
### Only Get HTTP Response Headers
```bash
curl -I <url>
```
### HTTP Generic Request

Change the type of the HTTP request using the `-X` flag followed by one of: `GET`, `POST`, `DELETE`, `PUT`.

To provide query parameters to the `<url>` add the `-d` option

```bash
curl -d "what=nobs&book=techbook" -X <url>
```

### HTTP POST Request Sending JSON

Set the Content-Type header with the `-H` flag

```bash
curl -d '{"what": "nobs", "book": "techbook"}' -H "Content-Type: application/json" -X POST <url>
```

The contents from a JSON file can also be used
```bash
curl -d "@content.json" -X POST <url>
```

### Follow a Redirect

When a redirect response (e.g. status code 301) contains the `Location` header field, the redirect can be followed with the `-L` flag

```bash
curl -L <url>
```

### Store Response to a File

The `-o` flag saves the response to the file specified while the `-O` flag saves it using the filename on the server.

```bash
curl -o output.html <url>
```
or
```bash
curl -O <url>/index.html
```

### HTTP Authentication

```bash
curl -u <username>:<password> <url>
```

### Additional notes

- Use the `--verbose` option to provide all information about the request and response




