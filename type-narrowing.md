
# Type Narrowing in TypeScript

## Introduction

When a variable can hold more than one type, TypeScript will not let you call a method that exists on only one of them. Type narrowing is how you prove to the compiler which type you actually have at a certain point in the code. Inside a narrowed block, TypeScript treats the variable as the more specific type, so you get correct autocomplete and safety.

## Narrowing with `typeof`

`typeof` is the right tool for primitive types like `string`, `number` and `boolean`.

```ts
function formatId(id: string | number): string {
  if (typeof id === "string") {
    return id.toUpperCase();
  }
  return id.toFixed(0);
}
```

Inside the `if`, `id` is a `string`. After that branch returns, TypeScript knows only `number` is left.

## Narrowing with `instanceof`

For class instances, `instanceof` checks whether an object was created from a specific class.

```ts
function getMessage(error: Error | string): string {
  if (error instanceof Error) {
    return error.message;
  }
  return error;
}
```

## Narrowing with `in`

When two object types have different properties, the `in` operator checks which property exists.

```ts
interface Car { drive(): void }
interface Boat { sail(): void }

function move(vehicle: Car | Boat): void {
  if ("drive" in vehicle) {
    vehicle.drive();
  } else {
    vehicle.sail();
  }
}
```

## Conclusion

Type narrowing lets one function safely handle several types. Use `typeof` for primitives, `instanceof` for classes and `in` for plain objects, and TypeScript will catch type mistakes before your code ever runs.
