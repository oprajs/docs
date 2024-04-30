---
sidebar_position: 2
---

# Simple Types

## Understanding Simple Types in Opra
In the realm of database management, the concept  of simple types froms the cornerstone for organizing and storing data efficiently wihtin the Opra framework. Let's explore what edfines simple types, how the are defined and their significance in datase design.

### Introduction
Simple Types are the elemental units of data recognized and stored within the Opra database system. These types encompass fundamental data categories such as integers, floats, booleans and strings. They represent the smalles, indivisible components upon which more complex data structures are built.

:::info
For instance, consider the following simple types:
```
Integer: Represent whole numbers without fractional parts.

Float: Represent numbers with fractional parts.

Boolean: Represent logical values of true or false.

String: Represent sequences of characters.
```

These simple types serve as the building blocks for constructing more intricate data representations within database records.
:::

## Significance in Database Design
Understanding simple types is crucial for designing efficient database schemas and querying data effectively within the Opra framework. By leveraging these elemental data units, developers can construct complex data structures that accurately represent real-world entities and relationships.

For instance, a database schema might include tables with columns defined using various simple types to represent attributes of different entities. By organizing data in this manner, it becomes easier to manage, query, and analyze information within the database.

In conclusion, simple types form the foundational elements of data representation in Opra, enabling developers to create robust and efficient database systems capable of handling diverse data requirements.

### Using Simple Types

In Opra, simple types are defined with specific characteristics that govern their behavior and usage. Let's take a look at how each simple type can be defined:

```jsx
name: string;
age: Integer;
weight: Float;
is_active: Boolean;
```

The example above is a Simple Type. Now let's explain it in detail here.
:::info
`@ApiField`: The smallest data is specified with this parameter. `ApiFields` combine to form a Complex Type.
:::
:::info
`name: string;`: The content of our data. Here we want name to be a string value.
:::

Let's see below how I created a phone number page with Simple Types. So that it is more understandable.

```jsx
import { ApiField, ComplexType } from '@opra/common';

@ComplexType()
export class PhoneNumber {

  @ApiField({type: 'number'})
  areaCode: number;

  @ApiField({type: 'string'}})
  phoneNumber: string;
}
```

Above we have set up a structure written with a simple Opra library.

```jsx
import { ApiField, ComplexType } from '@opra/common';
```

Above are the structures we need to make from the Opra foundations.

```jsx
@ComplexType()
export class PhoneNumber{
}
```
Above we show how to export the structure we have created.


### Defining a Simple Type

Simple Types are used to represent specific data categories and are often basic data types or data structures created for a specific purpose.

For example, let's say we want to define a Simple TYpe to represent the age of a user. We can do this using TypeScript as shown below:

```jsx
// /models/types/id.ts
import { isString, vg } from 'valgen'; // valgen library import
import type { ExecutionOptions } from 'valgen/typings/core/types';
import { SimpleType } from '@opra/common';

const_isId =
  vg.pipe<string>(
    isString,
    vg.isRegExp(/^[a-z0-9]{25}$/, {
      formatName: 'id',
      onFail: () => '{{label}} is not a valid "id" value'
    })
  );

@SimpleType({
  name:'id',
  description: 'An Unique Identifier (UID) value',
  decoder: _isId,
  encoder: _isId
})
export class IdType {
  static isID(value: any, options?: ExecutionOptions):
    string {
      return _isId(value, options);
  }
}
```

### Using a Defined Simple Type

At this point we create a SimpleType called IdType. We will use this Type when saving data in the database. For example, let's define an opraId below.

```jsx
// opra.ts
@ApiField({
  readonly: true;
  type: "id"
})
opraId?: IdType;
```

:::info
OpraId is now defined as a value

opraId?: IdType;
:::

Let's use it in a service file to generate the OpraId.

```jsx
// opra.service.ts
idGenerator: IdType.generateId,
```

We now have data in the database that is generated and appears on the screen as opraId.


## Field Interface in Simple Type

We use Field Interface to make more detailed use in Simple Types. This is an advantage of the Opra library.

```jsx
@ApiField({
  // Used at this point
})
opra: string;
```

:::info
Below are these Field Interfaces.

`type`: type

`description?: string;`: Defines the description of the field

`isArray?: boolean;`: Indicates if the field value is an array

`default?: any;`: Defines the default value of the field

`fixed?: string | number | boolean;`: Indicates the fixed value of the field. The value of the field can not be any other value.

`required?: boolean;`: Indicates if field value required in create operation

`readonly?: boolean;`: Indicates if the field is readonly

`writeonly?: boolean;`: Indicates if the field is writeonly

`exclusive?: boolean;`: If true, this Field will not be included in results by default.
The client side should include the Field name in the "include" query parameter.

`translatable?: boolean;`: If true, this Field is a candidate for translations

`examples?: any[] | Record<string, any>;`: Defines example values for the field

`deprecated?: boolean | string;`: Indicates if the field is deprecated and can be removed in the next

`pattern?: string;`: Defines RegExp pattern for the field. A String type is required for this option

`partialUpdate?: boolean;`: Indicates if partial update enabled for this field
:::

These field interfaces play a crucial role in defining the structure and behavior of fields within the system. By utilizing these interfaces effectively, developers can ensure clarity, consistency, and flexibility in data management and manipulation operations.