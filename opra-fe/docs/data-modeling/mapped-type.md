---
sidebar_position: 5
---

# Mapped Types

## Mapped Types in Opra
Mapped types stand as foundational elements within the Opra database system, offering a versatile approach to managing diverse datasets during te data modeling process. These types empower users with the capability to merge disparate data sources seamlessly or to selectively extract specific data elements from a JSON dataset, thereby enchacing the flexibility and adaptability of data representation within the Opra framework.

### Introduction
Mapped types serve as idispensable tools for navigating the complexities inherent in modern data modeling endeavors. By providing mechanisms for combining or extracting data elements from various sources, these types facilitate the creation of comprehensive and cohesive data models that accuratly reflect the underlying dataset's structure and relationships.

### Application
One common application of mapped types is their utilizaition in integrating data from multiple sources. Through the amalgamation of data usning pick parts, users can effortlessly merge datasets with complementary information, thereby enriching the overall dataset and enchancing its utility for analysis and decision-making processes.

Additionally, mapped types offer the ability to selectively omit specific data elemetns from a JSON dataset, tailoring the resulting dataset to suit specific analytical or operational requirements. This selective extraction capability ensures that users can focus on pertinent data elements while discrading extraneous information, thereby optimizing the effeciency and effectiveness of data processing tasks within the OPra environment.

### Conclusion
In conclusion, mapped types represent a powerful and flexible mechanism ffor managing data within the Opra database system. Whether through the concolidation of disparate datasets or the selective extraction of data elements, these types empower users with the tools needed to create robust and insightful data models that drive informed decision-making and facilitate organizational success.


## Using Mapping Types

### `Pick`
The `pick` utility type creates a new subtype by selecting specific properties from an existing type. It is useful when only certain properties are needed from a type, enhancing code readability.

### `Omit`
The `Omit` utility type generates a new subtype by excluding specified properties from an existing type. It is used when creating a new type by excluding certain properties from the original type.

### `Partial`
The `Partial` utility type creates a new subtype by making all properties optional from an existing type. It offers a flexible approach when partially filling or making all properties optional in a specific type, often used when dealing with objects or data structures, providing flexibility in filling or not filling.

Opra, if you have a Complex Type in front of you and you want to get custom data from it. It gives you the Pick ability. When you do this, you Picked the data. Here in example:

### `PartialSome`
The `PartialSome` utility type forms a new subtype by making specific properties optional or required from an existing type. It provides flexibility by making selected properties optional or mandatory.

### `StrictOmit`
The `StrictOmit` utility type, similar to Omit, ensures that only the specified properties exist in the resulting type, excluding all other properties from the original type, enforcing stricter type control.


## Examples
Below is an example Complex Type:

```jsx
// address.ts
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

:::info
Above we have a complete Complex Type page. Now let's pull certain data from here.
:::

### Using Pick in Mapped Types

```jsx
// adress.service.ts
async createAdress (
  info: Pick<Address, 'city' | 'street' | 'countryCode'>
)
```
:::info
When making the pick above, we get the data from the `Address` complex structure. We specifically pull the `city`, `street`, `countryCode` values as content.
:::

### Using Omit in Mapped Types

```jsx
// adress.service.ts
async createAdress (
  info: Omit<Address, 'city'>
)
```
:::info
When making the pick above, we get the data from the `Address` complex structure. Here, we can eliminate the details that we do not want from the data with omit. For example, we wanted to omit the `city` detail. Now when we want to use simple types from this complex structure, we will exclude `city`.

:::

### Paritalsome in Mapped Types

When working with Opra, you may encounter situations where you need to define specific subsets of properties from an interface or a class. This is where Opra's utility types come in handy.

Consider the following TypeScript.
```jsx
export class User {

  @ApiField({description: 'Name'})
  name: string;

  @ApiField({description: 'Age'})
  age: number;

  @ApiField({description: 'Email'})
  email: string;

}
```

Suppose you have a method `createUser` that only requires the `name` field from the `User` class. You can achieve this by using the `Pick` type:

```jsx
async createUser (
  info: Pick<userDto, 'name'>
)
```

Now, let's say you have another method `partialCreateUser` where you want to accept partial information for creating a user. You can use the `Partial` type for this purpose:

```jsx
async partialCreateUser (
  info: Partial<createUser>
)
```

However, what if you want `partialCreateUser` to accept only partial information but ensure that certain field are mandatory? This is where the `PartialSome` type comes into play:

```jsx
async partialCreateUser (
  info: PartialSome<createUser, 'name' | 'age'>
)
```

By using `PartialSome`, you can achieve a fine-grained control over which fields are required and which ones are optional whren dealing with partial objects. This enhances type safety and helps prevent runtime errors in your TypeScript codebase.

### StrictOmit in Mapped Types

The StrictOmit helper type works similarly to Omit, but ensures that the new type created contains only the specified properties. This ensures that unspecified properties are not included in the created type.

```jsx
type SıkıAtlananTip = StrictOmit<BenimTipim, 'name' | 'age'>;
```

In the example above, StrictOmittedType is a new type created by omitting the 'name' and 'age' attributes from the MyType type. However, unlike Omit, the type created is restricted to include only 'name' and 'age' properties. Other properties of MyType will not be included in this type.