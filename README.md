# EStruct

estruct traverses javascript projects and maps all the dependencies and relationships to a JSON. the output can be used to build network visualizations of the project and document the architecture.

---

Getting started

```shell
go get github.com/RayLuxembourg/estruct
```

```go
root := "/path/to/project/src"
labels:= make([]estruct.Label,0) // or create real labels
p:= estruct.NewConfig(root, `(.(js|jsx))$`,labels)
relativePath := "./src"
datasets, fileMap, dependenciesMap := p.Init(relativePath) // the output is the json
```

Saving output to a json file

```go
jsonName := "application.json"
os.Remove(jsonName)
b, _ := json.Marshal(datasets)

ioutil.WriteFile(jsonName, b, 0666)
```

Output json structure

```json
[
  {
    "id": "52FDFC07-2182-654F-163F-5F0F9A621D72",
    "path": "/Users/myUser/work/myProject/src/Component.js",
    "dependencies": [
      "__webpack_public_path__",
      "react",
      "react-dom",
      "app-data"
    ],
    "folder": "src",
    "extension": "js",
    "name": "ECMComponent",
    "lines": 106,
    "label": ""
  },
  {
    "id": "9566C74D-1003-7C4D-7BBB-0407D1E2C649",
    "path": "/Users/myUser/work/myProject/src/__webpack_public_path__.js",
    "dependencies": [],
    "folder": "src",
    "extension": "js",
    "name": "__webpack_public_path__",
    "lines": 3,
    "label": ""
  },
  {
    "id": "81855AD8-681D-0D86-D1E9-1E00167939CB",
    "path": "/Users/myUser/work/myProject/src/app-data.jsx",
    "dependencies": [],
    "folder": "src",
    "extension": "jsx",
    "name": "app-data",
    "lines": 4,
    "label": ""
  }
]
```

EStruct will generate unique id for each mapped file to allow relationship creation using those id's

### How is this helpful to your organization ?

Using the output of EStruct, you can visualize your complex large scale JavaScript project using tools like neo4j and
then ask real world questions from the graph database.
![](https://i.imgur.com/uUzJeCL.png)

You can also integrate the EStruct with your devops pipeline to keep track of your project architecture and changes.

### Todo list

- [x] Parse ES Modules
- [ ] Support CommonJS
- [ ] Generate labels based on user patterns (analyze file name and decide which label to give it)
- [ ] Add support for require syntax.
- [ ] Create CLI tool
- [ ] Publish using NPM
- [ ] Read configuration from project root directory .estructrc.json
- [ ] Boost performance
- [ ] Cleaner code
- [ ] make EStruct plugable/extendable to support various project structures
- [ ] use lexer and parsers to support multiple ecmascript versions and retrive more data about the contents of the code.

