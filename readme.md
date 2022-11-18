# Uuid
[[عربي]](readme.ar.md)

Alusus bindings for libuuid.

## Adding to the Project

Import the library as follows:

```
import "Apm";
Apm.importFile("Alusus/Uuid");
```

## Functions

### generate

A fucntion for generating random uuid value. This function takes a reference to `uuid_t` and puts a random UUID in it.
```
function generate (uuid: ref[uuid_t]);
```

### compare

Compares two uuid values. It return 0 if they are equal, and 1 otherwise.
```
function compare (uuid1: ref[uuid_t], uuid2: ref[uuid_t]): Int;
```

### clear

A function for clearing a uuid. The value in the variable after calling this function will be null.
```
function clear (uuid: ref[uuid_t]);
```

### copy

Copies the value of one uuid to another. It takes two uuid_t references and copies the value of the second to the first.
```
function copy(destUuid: ref[uuid_t], srcUuid: ref[uuid_t]);
```

### parse

Converts the uuid from a string to a uuid_t. Returns 0 on success, -1 otherwise.
```
function parse(src: ptr[array[char]], dest: ref[uuid_t]): Int;
```

### unparse

Converts the uuid from a uuid_t type to a string.
```
function unparse(uuid: ref[uuid_t], out: ptr[array[char]]);
```

### isNull

A function to check if the value of a uuid_t variable is null or not, it returns 1 if it is null, and 0 otherwise.
```
function isNull(uuid: ref[uuid_t]): Int;
```
 


## Example

```
import "Srl/Console";
import "Apm";
Apm.importFile("Alusus/Uuid");

func test {
    use Uuid;
    use Srl.Console;

    def u1: uuid_t;
    def u2: uuid_t;
    def str: array[char, 100];

    // Generate a random UUID.
    generate(u1);

    // We need to convert the value to a string before we can print it.
    unparse(u1, str~ptr);
    print("Randomly generated UUID: %s\n", str~ptr);

    // Output will be something like this:
    // Randomly generated UUID as array of chars: 5126ead0-be18-494f-a403-034c75d9cf93 

    print("clearning the uuid\n");
    clear(u2);

    // Check if the uuid has been cleared.
    if isNull(u2) == 1 print("uuid is cleared!\n")
    else print("uuid is not cleared\n");

    // output:
    // clearning the uuid
    // uuid is cleared!

    print("Enter Uuid as a string: ");
    getString(str~ptr, 100);

    // Convert to uuid_t
    parse(str~ptr, u2);

    // Did the user enter the same value as the generated one?
    if compare (u1, u2) == 0 print("u1 and u2 are equal.\n")
    else print("u1 and u2 are not equal.\n");

    copy(u1, u2);
    
    if compare (u1, u2) == 0 print("u1 and u2 are equal.\n")
    else print("u1 and u2 are not equal.\n");

    // Output will be:
    // u1 and u2 are equal.
}

test();
```

