---
layout: post
title: "Neo4j with python: meet problem when connecting to the local server"
excerpt: ""
tags:
  - GraphDatabase
  - EN

---



- I took the first bite of Neo4j today using python, I meet the error

  ```
  raise MaxRetryError(_pool, url, error or ResponseError(cause))
  ```

  when I ran the code 

  ```
  from py2neo import Graph,Node,Relationship
  ##
  test_graph=Graph(
      "http://localhost:7474",
      username="neo4j",
      password="neo4j"
  )
  
  ##
  test_node_1 = Node(label = "Person",name = "test_node_1")
  test_graph.create(test_node_1) # error pops up here
  
  ```

  things similar happen with neo4j (the official driver). I realized that it is the connection issue and here is the solution.

  

- launch a cmd (windows) or a terminal and initialize the port before create the connection

- Note that things work differently in python 2.x and python 3.x, for python 2.x, go

```bash
python  -m SimpleHTTPServer [port] 
```

- for python 3.x, go

```
python -m http.server [port]
```

- in the case the port number is `7474`



-----

- [ref](<https://appdividend.com/2019/02/06/python-simplehttpserver-tutorial-with-example-http-request-handler/>)
- similar questions
  - [1](<https://github.com/appium/appium/issues/11898>), [2](<https://stackoverflow.com/questions/49540888/connection-error-py2neo-python-3-win10-64-bit>) and thanks to user3701979's inspiration