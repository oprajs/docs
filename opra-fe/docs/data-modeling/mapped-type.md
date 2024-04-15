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


## Using Pick in Mapping Types
Opra, if you have a Complex Type in front of you and you want to get custom data from it. It gives you the Pick ability. When you do this, you Picked the data. Here in example:


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
```jsx
// adress.service.ts
async createAdress {
info: Pick<City, 'city' | 'street' | 'countryCode'>
}
```
:::info
When making the pick above, we get the data from the city complex structure. We specifically pull the city, street, countryCode values as content.
:::

## Using Omit in Mapping Types