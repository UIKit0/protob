# Protob

Protocol buffers for Node.js.

## Protofile

The command line file 'protob' will compile your protocol buffers and output them

### Usage

Define a protos.json file:

    [
      {
        "local": "path/to/protos/directory",
        "paths": {
          "relative/path" : ["specific/path"]
        }
      },
      {
        "git": "git@git.squareup.com:some/protos_repo.git",
        "paths": {
          "relative/path": ["specific", "paths"]
        }
      }
    ]

    $> protob --help
    $> protob

This will compile your protocol buffer definitions to json for the protob library to consume.

You can also use this directly.

    $> protoc --json_out=./some/path -I some/path some/proto/files

## Protocompiler

This will compile your protocol buffers into Javascript objects.

You can access your protocol buffers either by the registry or object cache.

    var Protob = require('protob').Protob;
    var Compiler = require('protob').Compiler;
    Compiler.compile();
    var registry = Protob.registry;
    var protos = Protob.v;

    myMessage = new r['some.package.MyMessage']({with: "values"});
    myMessage = protos.some.package.MyMessage({with: "values"});

## Encoding / Decoding

    myMessage.encode(); // encodes to a buffer ready to be sent
    MyMessage.decode(myMessage.encode()); // decodes from a buffer to a message
    myMessage.allFields; // provides a cooerced version of the message. 64 bit integers use the Long library

## Reflection

Messages are stored with their descriptor available on their constructor.

MyMessage.descriptor // access the definition of the protocol buffer

## ENUMS

You can set an enum value as either the number of name.

    myMessage.enum_value = "FOO"
    myMessage.encode() // will do the right thing