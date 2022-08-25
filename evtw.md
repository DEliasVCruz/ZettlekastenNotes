# lang.py.module.serialize.json

Work with serialized data in json format

## Synopsis

```py
  import json

  data = <data>
  serialized_data = json.loads(data)
  deserialized_data = json.dumps(serialized_data)
```

## Overview

You can use `json` to store and exchange data across a network; and the
`Python` json library aids you to serialize (write/encode) and deserialize
(read/decode) json data

## Cookbook

### Write json data

You can write your native `Python` data structures into json with:

- `dump(<data-obj>, <file-obj>)`: Write into a `.json` file
- `dumps(<data-obj>)`: Write into a [string](./4t3v.md) representation of json data

This process is also referred to as `serialization` or `encoding`

```py
  data = {
      'Person': {
        'Name': 'Daniel',
        'Age': 23,
        'Programs': ['Python', 'SQL', 'VBA'],
      }
    }

  with open('file.json', mode='w') as write_file:
      json.dump(data, write_file)                   # Write the data to a file

  json_string = json.dumps(data)                    # Json as string object
```

### Read json data

You can read from json data to native `Python` data structures with:

- `load()`: Read from a json file
- `loads()`: Read from a string representation of json data

This process is also referred to as `deserialization` or `decoding`

```py
  with open('file.json', mode='r') as read_file:
      data = json.load(read_file)                   # Load json from a file

  json_str = """
  {
      'Person': {
          'Name': 'Daniel',
          'Age': 23,
          'Programs': ['Python', 'SQL', 'VBA']
        }
    }
  """"

  data = json.loads(json_str)                       # Load from a json as string
```

### Parse json data

Once you've loaded a json object, be it by loding it from a file or
a string. You can then access it's contentens as a nested set of
dictionaries and lists

```py
  json_str = """
  {
      'Person': {
          'Name': 'Daniel',
          'Age': 23,
          'Programs': ['Python', 'SQL', 'VBA']
        }
    }
  """"

  data = json.loads(json_str)
  data["Person"]["Name"]                            # Daniel
  data["Person"]["Programs"][0]                     # Python
```

### Create a custom encoder function

If you got a complex object that you want to serialize, by **default** the
built-in json encoder **can't** do it and **will throw an exception**

But you can provide your own encoding function by **passing it to** the
`default=` parameter

```py
  def encode_complex(z):
      if isinstance(z, complex):
          data = {
              '__complex__': True,          # Metadata for object recreation
              'real': z.real,
              'imag': z.imag
            }
          return data
      else:
            type_name = z.__class__.__name__
            raise TypeError(f"Object of type '{type_name}' is not JSON serializable")

  print(json.dumps(9 + 5j, defulat=encode_complex))
  # '{ '__complex__': True, 'real': z.real, 'imag': z.imag }'
```

### Create a custom encoder class

Another way to create a decoder for a complex object is by creating a subclass
decoder that inherits from the `json.JSONEncoder` and modifies the `default()` method

```py
  class ComplexEncoder(json.JSONEncoder):
      def default(self, z):
          if isinstance(z, complex):
              data = {
                  '__complex__': True,      # Metadata for object recreation
                  'real': z.real,
                  'imag': z.imag
                }
              return data
          else:
              return super().default(z)

  complex_encoder = ComplexEncoder()
  print(complex_encoder.encode(3 + 6j))
  # '{ '__complex__': True, 'real': z.real, 'imag': z.imag }'
```

### Create a custom decoder function

Every time the `load()` functions attempts to parse an object you can **intercede
before the default decoder**  with the `object_hook=` parameter

You can use this to pass a custom decoder function, and can work with more than
one object at a time

```py
  def decode_complex(dct):
      if dct['__complex__']:
          return complex(dct["real"], dct["imag"])
      return dct

  with open("complex_data.json") as complex_data:
      data = complex_data.read()
      z = json.loads(data, object_hook=decode_complex)
```
