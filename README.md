# libdataobj
C++ Data structures container

Example Use:
```
    #include <libdataobj/DataObject.h>
    using namespace dataobject;
...

## Define json like structures and access it easily
# Definition
```
    DataObject obj;
    obj["int"] = 0;
    obj["double"] = 2.1;
    obj["string"] = "sample text";
    obj["array"].addArrayObject(sDataObject("sub data object"));
    obj["object"]["key"] = 4;
    obj["object"]["key2"] = "string";
```

# Iterations
```
    for (auto const& el : obj.getSubObjects())
    {
        if (el->type() == DataType::String)
            std::cerr << el->getKey() << " " << el->asString();
    }

```

# Pointers of data
```
    spDataObject obj;
    (*obj)["data1"] = "text";
    (*obj)["data2"] = "text";

    spDataObject obj2;
    (*obj2)["data"] = "text";
    (*obj2).atKeyPointer("sub data object") = obj;
```

# Read
```
    std::string str = R"(
      {
      "logs": [
          {
           "address": "0x0f572e5295c57f15886f9b263e2f6d2d6c7b5ec6",
           "topics": [
            "0x000000000000000000000000095e7baea6a6c7c4c2dfeb977efac326af552d87"
           ],
           "logIndex": "0x0",
           "removed": false
          }
         ]
      }
    )";

    spDataObject a = ConvertJsoncppStringToData(str);
    assert(a->atKey("logs").at(0).atKey("removed").asBool() == false);
```

# Print
```
std::cout << obj.asJson() << std::endl;
{
    "int" : 0,
    "double" : 2.1000,
    "string" : "sample text",
    "array" : [
        "sub data object"
    ],
    "object" : {
        "key" : 4,
        "key2" : "string"
    }
}
```
