[![fuzz-removebg-preview.png](https://i.postimg.cc/VsxCTCxS/fuzz-removebg-preview.png)](https://postimg.cc/rz9sRKFc)

<hr />

## What is it?

GOFUZZ is fast web fuzzer which takes in URL as input and test the URL for diffrent set of inputs provided by the user.

<p align="center">
   <img src="https://i.postimg.cc/Mpmq7n2f/gofuzz-usage.png"/>
</p>

## TODO

- [ ] Add Output file feature where output can be stored in specified file
- [ ] Add export type option where output can be saved in JSON and CSV
- [ ] Add timeout feature when user one URL is not responding for a specific time
- [ ] Add Permuation feature

and a lot more... 

Will add as we go along

## Features

### Passing target URL to the fuzzer

Target URL has to be provided using `-u` option like so:

```bash
gofuzz -u "http://targeturl.com/targetpath?q1=<@>&q2=<@>"
```
**What is `<@>` ?**

`<@>` is placeholder where the test cases will be placed while fuzzing. We'll see how it works on the way.

### Fuzzing for numeric values

Numeric values can be passed using `-n` option like so:

- `-n 100` : tests from 0 to 100
- `-n 10,200` : tests from 10 to 200
- `-n 10,11,20,50` : tests for 10,11,20,50 only

```bash
gofuzz -u "httpL//targeturl.com/targetpath?q1=<@>&q2=<@>" -n 100
```

above tests URL from `0-100` replacing placeholders(`<@>`) with numbers. Here is an gif showing example:

Target URL is one of the CTF challenges in Hacker101 CTF:

<p align="center">
  <img src="https://i.imgur.com/PLDrYIk.gif" />
</p>

here our target url is `http://35.227.24.107/9447ef5c5c/page/<@>` and in the output you can see the placeholder `<@>` gets replaced by the numbers from `0-20`. Notice we get `404` and `200` status code in all the URLs except one `http://35.227.24.107/9447ef5c5c/page/3` which gives `403 forbidden`. Now you know what you have to do ;)

### Fuzzing for ASCII characters

Suppose I want to test a URL for vulnerabilites like SQL injection or LDAP injection. Common way to do it is test for `*,",',=...so on`. Doing it manually is no cool. Provide a range of ASCII values using `-a` option and rest is done by GOFUZZ.

- `-a 65` : tests for `A` only
- `-a 65,90` : tests from `A` to `Z`
- `-a 65,66,67,68` : tests for `A,B,C,D` only

Testing on a test server I made using node js.

<p align="center">
   <img src="https://i.imgur.com/A0lVXcC.gif" />
</p>

you can see gofuzz escapes the required characters and on the server end it receives the actual characters.

**Documentation in Progress...**