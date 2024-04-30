---
sidebar_position: 4
---

# Enum Types

## Understanding Enum Types in Opra

ENUM (Enumerated) types are a special data type that allows a variable to be one of a set of predefined constants. These constants represent a finite set of values that the variable can take. ENUM types are commonly used to improve code readability and maintainability by providing meaningful names to these predefined constants.

## Introduction to Enum Types

ENUM types are particularly useful when you have a variable that can only have a limited number of possible values. Instead of using arbitrary numbers or strings to represent these values, you can define them as constants within an ENUM type. This makes your code more self-explanatory and less error-prone.

:::info
Because they are constants, the names of an enum type's fields are in uppercase letters.
:::

### Syntax and Usage in Opra

To define an ENUM type in TypeScript, you use the `EnumType` keyword followed by the type name and a list of constant values enclosed in curly braces {}. By convention, ENUM field names are written in uppercase letters.

```jsx
// ../Enums/Gender.ts
import { EnumType } from '@opra/common';

export enum Gender {
    M = 'M',
    F = 'F',
}

EnumType(Gender, {
    name: 'Gender',
    description: 'The gender of a person',
    meanings: {
        M: 'Male',
        F: 'Female',
    }
})
```

#### Using

We can use this data that we have prepared here as a complex structure in another structure.

```jsx
// ../user.ts
@ApiField({
    enum: Gender,
    required: true
})
gender: Gender;
```