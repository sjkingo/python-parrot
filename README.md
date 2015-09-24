# python-parrot

[parrot](https://www.youtu.be/npjOSLCR2hE) is a simple HTTP server that responds to any valid GET
request with the file specified on the command line.

It is useful during testing (e.g. to mock out a server application),
or to do client testing. Both text and binary files are handlded correctly.

Its only dependency is the excellent [python-magic](https://github.com/ahupp/python-magic) library
for mime type guessing. It works on Python 3.

```
$ pip install python-parrot
```

## Usage

```
$ parrot port filename
```

The following arguments are required:

* `port`: Port to listen on
* `filename`: Filename of the data to send in response to all requests


## Sample

Start the parrot server:

```
$ echo 'This is a test' > test.txt
$ parrot 8000 test.txt
parrot/1.0.0 listening on 0.0.0.0:8000 with file test.txt (text/plain)
```

In another terminal (assuming `10.1.1.1` is a valid IP on the server):

```
$ echo 'GET /anything HTTP/1.0' | nc 10.1.1.1 8000
HTTP/1.0 200 OK
Server: parrot/1.0.0 Python/3.4.2
Date: Thu, 24 Sep 2015 00:27:56 GMT
Content-Type: text/plain

This is a test
```
