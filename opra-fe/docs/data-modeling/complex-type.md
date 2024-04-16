---
sidebar_position: 3
---

# Complex Types

## Understanding Complex Types in Opra
Complex types within the Opra database system are pivotal for handling composite or structured data, enabling the representation of intricate data structures built upon combinations of simple types. This section delves into the essence of complex types, their significance, and practical applications within the Opra framework.

### Introduction
Complex types encompass sophisticated data structures composed of combinations of simple types or other complex types. Unlike simple types, which represent elemental data units, complex types organize data into hierarchical structures, facilitating comprehensive data representation and manipulation.

### Example

Consider a scenario where a record a prime example of a complex type. A record encapsulates multiple fields, each capable of containing simple types or other complex types. This hierarchical arrangement enbasles the creation of structured data entities with diverse attributes and properties.

Similary, arrays and lists serve as complex types capable of storing collections of elements, each accomodating simple types or complex types. These data structures offer efficient management and manipulation of ordered data sets.

## Utilizing Complex Types

Below is an illustrative example demonstrating the implementation of a cpmplex type in Opra, providing insights into its structure and usage.

```jsx
import { ApiField, ComplexType } from '@opra/common';

@ComplexType({
  description: 'Address information'
})
export class Address {

  @ApiField({description: 'Country code'})
  countryCode: string;

  @ApiField({description: 'City name'})
  city: city;

  @ApiField({description: 'Street information'})
  street: string;

  @ApiField({description: 'ZIP code'})
  zipCode: string;

}
```

## Key Differences Between Complex and Simple Types

It's essential to discern the fine line distinguishing complex types from simple types within the Opra framework. Below, we elucidate this contrast through practical examples:

:::info
```jsx
  @ApiField({type: City})
  city: City;
```
In this example, city is defined as a complex type, potentially comprising multiple attributes encapsulated within the City structure.
:::

:::info
```jsx
  @ApiField({description: 'Street information'})
  street: string;
```
Contrarily, street represents a simple type, denoted by a singular attribute (string) conveying straightforward data.
:::

### Enhanced Understanding with Examples
To fortify comprehension, let's delve deeper into the intricacies of complex types by dissecting their attributes using comprehensive examples:

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

In this example, we construct a complex type PhoneNumber, comprising distinct fields (areaCode and phoneNumber) capable of accommodating diverse data types.

### Expanding Structures in Opra

In Opra, the ability to extend structures allows for the easy reuse of data across different parts of your application. By defining common data structures and extending them as needed, you can streamline your code and ensure consistency throughout your application.

```jsx
// ./record-entity.ts

import { ApiField, ComplexType } from '@opra/common';
import { Column, DataType, PrimaryKey } from '@sqb/connect';

@ComplexType({
  abstract: true,
  description: 'Abstract Record Model'
})
export class Record {

  @Column(DataType.INTEGER)
  @ApiField()
  @PrimaryKey()
  id: number;

  @Column()
  @ApiField()
  deleted?: boolean;

}
```

Below is an example with an extend section.

```jsx
// ./customer-note.entity.ts

import { ApiField, ComplexType} from '@opra/common';
import { Column, Entity } from '@sqb/connect';
import { Record } from './record.entity.js';

@ComplexType({
  description: 'Customer notes entity',
})
@Entity({tableName: 'customer_notes'})
export class CustomerNotes extends Record {

  @ApiField()
  @Column({notNull: true, fieldName: 'customer_id'})
  customerId: number;

  @ApiField()
  @Column({notNull: true})
  title: string;

  @ApiField()
  @Column()
  content: string;
}
```

#### Conclusion
Complex types are indispensable components within the Opra framework, empowering developers to model sophisticated data structures and relationships effectively. By leveraging complex types, developers can construct robust database schemas capable of handling diverse data requirements with finesse.