# Overview
This exercise is meant to showcase your technical abilities by pairing with a Gaggle software engineer to modify an existing codebase by adding a new feature.
* You will fork [this repository](https://github.com/gaggle-net/candidate-technical-assessment-pairing-exercise) and use [this issue](https://github.com/gaggle-net/candidate-technical-assessment-pairing-exercise/issues/1) as your requirements.
* You will pair with a Gaggle software engineer to implement the new feature.
* The code coverage should not decrease as new code is added.

# Application
This application is a Web Service responsible for providing contact information from our contact database. The application is a proof of concept and is currently using an embedded database that inserts default data on startup.

## Default Contact Data
| id | name |
| --- | --- |
| 1 | Bruce Wayne |
| 2 | Dick Grayson |
| 3 | Jason Todd |
| 4 | Selina Kyle |
| 5 | Oswald Cobblepot |
| 6 | Edward Nygma |

# Features
| Feature | Description | Endpoint |
| --- | --- | --- |
| Search By Id  | Retrieve a specific contact by referencing it's unique identifier. | /api/contacts/_{id}_ |
| Search By Name  | Retrieve one or more contacts by searching by name (full or partial).  | /api/contacts?name=_{name}_ |

# Build & Test Application
## Assumptions
* Java (8+) is installed (tested with openjdk version "1.8.0_275")
* Maven (3+) is installed (tested with Apache Maven 3.6.3)

## Compile and Execute Unit Tests
```shell
% mvn clean verify
```

## Run Application
```shell
% mvn spring-boot:run
```

## Test Application
You can test using a tool like [Postman](https://www.postman.com/), or even using [cURL](https://curl.se/docs/manpage.html) from the commandline.

### Examples using cURL
Search for a contact by their id.
```shell
% curl -i 'localhost:8080/api/contacts/1'
HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Sat, 31 Jul 2021 20:01:18 GMT

{"id":1,"name":"Bruce Wayne"}
```
Search for a contact by their name.
```shell
% curl -i 'localhost:8080/api/contacts?name=bruce'
HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Sat, 31 Jul 2021 20:02:24 GMT

[{"id":1,"name":"Bruce Wayne"}]
```
Search for a contact with an invalid id.
```shell
% curl -i 'localhost:8080/api/contacts/99999'
HTTP/1.1 404 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Sat, 31 Jul 2021 20:03:55 GMT

{"error":"No contact found with id = 99999","timestamp":"2021-07-31T20:03:55.860+00:00"}
```
Search for a contact with a name that doesn't exist.
```shell
% curl -i 'localhost:8080/api/contacts?name=bob'
HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Sat, 31 Jul 2021 20:05:04 GMT

[]
```
