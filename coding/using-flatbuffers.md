# Using Flatbuffers
 
 Note that the flatbuffers tutorials are phenomenal. This guide doesn't aim to replace them, but to provide a breif overview of how to use them.
 Links: https://google.github.io/flatbuffers/flatbuffers_guide_tutorial.htmlo


# Schemas

The work with flatbuffers you need to define a `schema`. This file tells flatbuffers what each data structure consists of and how it's formatted. Schemas are written in the _Interface Definition Language_ (IDL), which uses syntax similar to C style languages.

From the flatbuffer tutorial, here is an example schema:
```
// Defines the namespace the generated code will be given
namespace MyGame.Sample;  
 
// An enum that can be used in the schema is declared like this
enum Color:byte { Red = 0, Green, Blue = 2 }
 
// You can couple tables using the union keyword
union Equipment { Weapon, Backpack } // Optionally add more tables.
 
// Structs can also be used in the schema like this
struct Vec3 {
  x:float;
  y:float;
  z:float;
}

// This is the main object in the flatbuffer. It uses all the other
// components (enums, structs, tables) defined elsewhere in the schema
table Monster {
  pos:Vec3; // Struct.
  mana:short = 150;
  hp:short = 100;
  name:string;
  friendly:bool = false (deprecated);
  inventory:[ubyte];  // Vector of scalars.
  color:Color = Blue; // Enum.
  weapons:[Weapon];   // Vector of tables.
  equipped:Equipment; // Union.
  path:[Vec3];        // Vector of structs.
}
 
table Weapon {
  name:string;
  damage:short;
}

table Backpack {
    capacity:short;
}
 
// The root type declares the root table for the serialized data
root_type Monster;
```

# Compiling the Schema

Once you've defined your schema you have to compile with with `flatc`. If the above schema was called `monster.fbs`, this will generate a file called `monster_generated.h` (for C++) which should be included in whatever file you expect to conduct the serialization in.

# Reading and Writing Flatbuffers

First, create an instance of the `FlatBufferBuilder` which will contain the buffer as items are added to it.
```C++
flatbuffers::FlatBufferBuilder builder(1024);
```

Using the `builder` you can use the `CreateX` shortcut (where `X` is the name of the table) to build whole tables quickly. Any objects that are contained within the root table have to be serialized before they're added.

Optionally, you can add each element to the flatbuffer manually by creating a builder object for the specific table and then adding elements one-by-one

```C++
MonsterBuilder monster_builder(builder);
monster_builder.add_pos(&position);
monster_builder.add_hp(hp);
...
monster_builder.add_equipped_type(Equipment_Weapon);
monster_builder.add_equipped(axe.Union());
auto mon = monster_builder.Finish();
```
