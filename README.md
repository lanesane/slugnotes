SlugNote Server
===

# Description
Node server for SlugNote

# Requirements
- node.js
- mongoDB
- redis

# Installation
- Run `git clone https://*USER*@github.com/slugnote/slugnote.git`
- Run `npm install` in the 'slugnote' directory

# Running the app
    node server

# Documentation
## Usage
Send an HTTP POST method to the server at the URI of the desired command
with the body of the request being a valid JSON object (Like examples)

### With `curl`
    curl -k -H "content-type: application/json" -d "JSON OBJECT" https://169.233.236.39/URI
* -k 
    * Ignore the fact that we have a self-signed certificate (We should probably get a proper cert)
* -H "content-type: application/json"
    * This cannot change. Basically just sets an HTTP header telling the server this is JSON
* -d "JSON OBJECT"
    * Sets the body of the HTTP request. JSON OBJECT must be valid JSON and must be the JSON that corresponds with the correct request
* https://169.233.236.39/URI
    * The URL to post to. If you're testing, change api.slugnote.com to the ip address of the server. URI should be the URI of the request you're making. For example, `post/createNote/`

## Unauthenticated calls

### getTokenTTL
#### URI
`post/user/gettokenttl`

#### Request
    {
		"authToken" : "uxoDiXpwq5TlGxt88fcPW4S+h4U9eDcCLQTaHY4vh/UT69LuYploxHI6TUOE+PrTquhQIagC5TKJjY6O+3gEGg=="
    }

#### Response
    {
        "status" : 200,
        "call" :  "getTokenTTL",
        "data" : {
            "ttl": 53020
        }
    }

#### Example curl command:
     curl -H "content-type: application/json" -d "{\"authToken\":\"uxoDiXpwq5TlGxt88fcPW4S+h4U9eDcCLQTaHY4vh/UT69LuYploxHI6TUOE+PrTquhQIagC5TKJjY6O+3gEGg==\"}" https://169.233.236.39/post/user/gettokenttl -k

## Authenticated calls

### createNote
#### URI
`post/note/createnote`

#### Request
    {
        "authToken" : "Gk1nJqj2X+IppQ7K0710EzUBcZKsq1+l3bXdfIMxP8w1L3b+rG2Uf4SIO+42UTGhF2G8XZNuJUyh/ipx1HTG4w==",
        "noteUser" : "username",
        "noteTime" : "2014-03-29:10:10",
        "noteFormat" : "String, PDF, JPEG",
        "noteData" : [ "Array" ],
        "noteInfo" : {
            "name" : "Example Note",
            "description" : "This note is an example.",
            "class" : {
                "id" : 1234567,
                "name" : "Class Name"
            },
            "term" : {
                "id" : 012345,
                "name" : "{Season} Semester"
            },
            "teacher" : {
                "id" : 012345,
                "name" : "First Last"
            }
        }
    }

#### Response
    {
        "status" : 200,
        "call" : "createNote",
        "data" : {
            "noteId" : "533700001bd3b21d0eba3498"
    }

### getNoteInfo
#### URI
`post/note/getnoteinfo`

#### Request
    {
        "authToken" : "Gk1nJqj2X+IppQ7K0710EzUBcZKsq1+l3bXdfIMxP8w1L3b+rG2Uf4SIO+42UTGhF2G8XZNuJUyh/ipx1HTG4w==",
        "noteId" : "533700001bd3b21d0eba3498"
    }

#### Response
    {
        "status" : 200,
        "call" : "getNoteInfo",
        "data" : {
            "noteUser" : "username",
            "noteTime" : "2014-03-29:10:10",
            "noteFormat" : "String, PDF, JPEG",
            "noteInfo" : {
                "name" : "Example Note",
                "description" : "This note is an example.",
                "class" : {
                    "id" : 1234567,
                    "name" : "Class Name"
                },
                "term" : {
                    "id" : 012345,
                    "name" : "{Season} Semester"
                },
                "teacher" : {
                    "id" : 012345,
                    "name" : "First Last"
                }
            }
        }
    }

### getNote
#### URI
`post/note/getnote`

#### Request
    {
        "authToken" : "Gk1nJqj2X+IppQ7K0710EzUBcZKsq1+l3bXdfIMxP8w1L3b+rG2Uf4SIO+42UTGhF2G8XZNuJUyh/ipx1HTG4w==",
        "noteId" : "533700001bd3b21d0eba3498"
    }

#### Response
    {
        "status" : 200,
        "call" : "getNote",
        "data" : {
            "noteUser" : "username",
            "noteTime" : "2014-03-29:10:10",
            "noteFormat" : "String, PDF, JPEG",
            "noteData" : [ "Array" ],
            "noteInfo" : {
                "name" : "Example Note",
                "description" : "This note is an example.",
                "class" : {
                    "id" : 1234567,
                    "name" : "Class Name"
                },
                "term" : {
                    "id" : 012345,
                    "name" : "{Season} Semester"
                },
                "teacher" : {
                    "id" : 012345,
                    "name" : "First Last"
                }
            }
        }
    }


### createUser
#### URI
`post/user/createuser`

#### Request
    {
        "authToken" : "Gk1nJqj2X+IppQ7K0710EzUBcZKsq1+l3bXdfIMxP8w1L3b+rG2Uf4SIO+42UTGhF2G8XZNuJUyh/ipx1HTG4w==",
        "userName" : "First Last",
        "userEmail" : "abc@def.com",
        "userPassword" : "password"
    }

#### Response
    {
        "status" : 200,
        "call" : "createUser",
        "data" : {
            "authToken" : "Gk1nJqj2X+IppQ7K0710EzUBcZKsq1+l3bXdfIMxP8w1L3b+rG2Uf4SIO+42UTGhF2G8XZNuJUyh/ipx1HTG4w=="
            "userId" : "533700001bd3b21d0eba3498"
        }
    }


### getUserInfo
#### URI
`post/user/getuserinfo`

#### Request
    {
        "authToken" : "Gk1nJqj2X+IppQ7K0710EzUBcZKsq1+l3bXdfIMxP8w1L3b+rG2Uf4SIO+42UTGhF2G8XZNuJUyh/ipx1HTG4w==",
        "userId" : "533700001bd3b21d0eba3498"
    }

#### Response
    {
        "status" : 200,
        "call" : "getUserInfo",
        "data" : {
            "userId" : "533700001bd3b21d0eba3498",
            "userEmail" : "abc@def.com",
            "userName" : "First Last"
        }
    }


### createToken
#### URI
`post/user/createtoken`

#### Request
    {
        
    }

#### Response
    {
        "status" : 200,
        "call" : "createToken",
        "data" : {
            "authToken" : "Gk1nJqj2X+IppQ7K0710EzUBcZKsq1+l3bXdfIMxP8w1L3b+rG2Uf4SIO+42UTGhF2G8XZNuJUyh/ipx1HTG4w=="
        }
    }


### createUniversity
#### URI
`post/university/createuniversity`

#### Request
    {
        "authToken" : "Gk1nJqj2X+IppQ7K0710EzUBcZKsq1+l3bXdfIMxP8w1L3b+rG2Uf4SIO+42UTGhF2G8XZNuJUyh/ipx1HTG4w==",
        "universityName" : "UC Santa Cruz"
    }

#### Response
    {
        "status" : 200,
        "call" : "createUniversity",
        "data" : {
            "universityId" : "533700001bd3b21d0eba3498",
            "universityName" : "UC Santa Cruz"
        }
    }


### list
#### URI
`post/university/list`

#### Request
    {
        "authToken" : "Gk1nJqj2X+IppQ7K0710EzUBcZKsq1+l3bXdfIMxP8w1L3b+rG2Uf4SIO+42UTGhF2G8XZNuJUyh/ipx1HTG4w==",
        "universityId" : "533700001bd3b21d0eba3498"
    }

#### Response
    {
        "status" : 200,
        "call" : "getUniversityList",
        "data" : {
            "universityId" : "533700001bd3b21d0eba3498"
            "array" : { [
                "courseId" : "123958201bd3b21d0eba4521"
                "courseName" : "CMPS 12B"
            ] }
        }
    }
