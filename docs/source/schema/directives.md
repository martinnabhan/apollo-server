---
title: Directives
description: Configure GraphQL types, fields, and arguments
---

> Looking for Apollo Federation directives? See [Federation-specific GraphQL directives](/federation/federated-types/federated-directives/).

A **directive** decorates part of a GraphQL schema or operation with additional configuration. Tools like Apollo Server (and [Apollo Client](/react/local-state/managing-state-with-field-policies/#querying)) can read a GraphQL document's directives and perform custom logic as appropriate.

Directives are preceded by the `@` character, like so:

```graphql {2} title="schema.graphql"
type ExampleType {
  oldField: String @deprecated(reason: "Use `newField`.")
  newField: String
}
```

This example shows the `@deprecated` directive, which is a [default directive](#default-directives) (i.e., it's part of the [GraphQL specification](http://spec.graphql.org/June2018/#sec--deprecated)). It demonstrates the following about directives:

- Directives can take arguments of their own (`reason` in this case).
- Directives appear _after_ the declaration of what they decorate (the `oldField` field in this case)

## Valid locations

Each directive can only appear in _certain_ locations within a GraphQL schema or operation. These locations are listed in the directive's definition.

For example, here's the GraphQL spec's definition of the `@deprecated` directive:

```graphql
directive @deprecated(
  reason: String = "No longer supported"
) on FIELD_DEFINITION | ARGUMENT_DEFINITION | INPUT_FIELD_DEFINITION | ENUM_VALUE
```

This indicates that `@deprecated` can decorate any of the four listed locations. Also note that its `reason` argument is optional and provides a default value. Usage examples of each location are provided below:

```graphql title="schema.graphql"
# ARGUMENT_DEFINITION
# Note: @deprecated arguments _must_ be optional.
directive @withDeprecatedArgs(
  deprecatedArg: String @deprecated(reason: "Use `newArg`")
  newArg: String
) on FIELD

type MyType {
  # ARGUMENT_DEFINITION (alternate example on a field's args)
  fieldWithDeprecatedArgs(name: String! @deprecated): String
  # FIELD_DEFINITION
  deprecatedField: String @deprecated
}

enum MyEnum {
  # ENUM_VALUE
  OLD_VALUE @deprecated(reason: "Use `NEW_VALUE`.")
  NEW_VALUE
}

input SomeInputType {
  nonDeprecated: String
  # INPUT_FIELD_DEFINITION
  deprecated: String @deprecated
}
```

If `@deprecated` appears elsewhere in a GraphQL document, it produces an error.

> If you create a custom directive, you need to define it (and its valid locations) in your schema. You don't need to define [default directives](#default-directives) like `@deprecated`.

### Schema directives vs. operation directives

Usually, a given directive appears _exclusively_ in GraphQL schemas or _exclusively_ in GraphQL operations (rarely both, although the spec allows this).

For example, among the [default directives](#default-directives), `@deprecated` is a schema-exclusive directive and `@skip` and `@include` are operation-exclusive directives.

The [GraphQL spec](https://spec.graphql.org/June2018/#sec-Type-System.Directives) lists all possible directive locations. Schema locations are listed under `TypeSystemDirectiveLocation`, and operation locations are listed under `ExecutableDirectiveLocation`.

## Default directives

The [GraphQL specification](http://spec.graphql.org/June2018/#sec-Type-System.Directives) defines the following default directives:

| Directive | Description |
|-----------|-------------|
| `@deprecated(reason: String)` | Marks the schema definition of a field or enum value as deprecated with an optional reason. |
| `@skip(if: Boolean!)` | If `true`, the decorated field or fragment in an operation is _not_ resolved by the GraphQL server. |
| `@include(if: Boolean!)` | If `false`, the decorated field or fragment in an operation is _not_ resolved by the GraphQL server. |
