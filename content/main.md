# HiBON

*Fast, serializable, hash-invariant data format*

---

<br>

Hash-invariant Binary Object Notation (HiBON)
is a data format inspired by [BSON](http://bsonspec.org/) and developed for the [Tagion network](tagion.org).


It is defined by the charateristic that it is.
1. Hash-invariant, the format specifies ordering, such that two pieces of the same data will produce the same hash.
2. Binary, meaning that it's compact, easy to serialize and decode. So it can be sent across a network and be verified on the receiving end quickly and easily, even on a hardware level.
3. Object-notation, which means that it a structued format, with keys and values common to most programming languags.
4. HIBON sounds cool


Along with that it defines a JSON compatible interchange format called HiBONJSON.  
A format for doing remote procedure calls called HiRPC.  
And an extension format for creating schemas called HiBONRecord.

## Usage examples in D-lang

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

## Specification

 * [Hash-invariant Binary Object Notation (HiBON)](/hibon)  
 * [Integer stream encoding (LEB128)](/leb128)
 * [JSON interchange format (HiBONJSON)](/hibonjson)  
 * [HiBON Remote Procedure Call (HiRPC)](/hirpc)  
 * [(UNDOCUMENTED) (HiBONRecord)](/hibonrecord)  
