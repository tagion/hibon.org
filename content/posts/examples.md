---
title: API Examples
---

# Usage examples in D-lang

For the full hibon D api documentation see [HiBON ddoc](https://ddoc.tagion.org/tagion.hibon.html)

Object interface

```d
// Create an hibon
auto hibon = new HiBON;

// Asign something to a key
hibon["hai"] = "bon";

// Create a serialized `Document` buffer
hibon.toDoc;
```

Lazy serialized documents

```d
// Where data is some ubyte[] received from the network or serialized directly from a hibon
// Creates a handler for the serialized data
auto doc = Document(data)

// Get a string value from the buffer
string decoded = doc["hai"].get!string;
```

HiBONRecords (schemas)

```d
// Defines the record name
@recordType("myRecord")
struct MyRecord {

    // Define a label with the name "hai"
    @label("hai") string str;

    // Turn the struct into a HiBONRecord type
    mixin HiBONRecord;
}

// Check if the data actually matches the record type
if (data.isRecord!MyRecord) {

    // Create an instance of the record with data
    auto record = MyRecord(data);

    // Get the value str
    record.str;
}
```
