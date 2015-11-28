# Data Types

#### int

An integer number with a maximum value of 2147483647\. Negatives are disallowed unless otherwise specified.

#### decimal(M, D)

A decimal number of up to M digits in total including* D* digits after the decimal point. Negatives are disallowed unless otherwise specified.

#### string(M)

A string of text up to M characters in length.

#### text

A string of text up to ~16,777,216 bytes in length.

#### boolean

A boolean value: true or false. In JSON it will be represented using the native boolean type. In XML, it will be the literal strings true or false.

#### date

An RFC 2822 date. All dates output by BigCommerce API responses are in GMT (+0000) time. However, any time zone may be used on inputs as the offset information will be converted accordingly.

#### datetime

An ISO 8601 datetime value. This is currently only supported as an input parameter on filters. Date values in responses remain in the RFC 2822 format.

#### enum

An enumeration of string values. Only the values specified in the fields description are allowed.

#### object

An object with its own set of fields.

#### country code

A 2 character ISO 3166-1 alpha-2 country code.

#### email address

A valid email address. 250 characters maximum.

#### variable

Variable data depending on context. See the field definition for specifics.

#### array

A simple list of values. In JSON this will be an array. In XML the field will contain a set of `<value>` elements.

#### resource

A string representing a URI reference to another resource within the current version of the API.

#### null

A null value. In JSON this is represented as the native null type. In XML, it is represented as the literal string NULL.
