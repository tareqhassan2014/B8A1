

# Generics and `Promise<T>` in TypeScript

## Introduction

Generics let you write a function, class or type once and reuse it with many different types without losing type information. Instead of hard-coding `string` or falling back to `any`, you add a type parameter, usually called `T`, which is filled in when the code is used.

## How Generics Work

```ts
function firstItem<T>(items: T[]): T | undefined {
  return items[0];
}

const city = firstItem(["Satkhira", "Khulna"]); // string | undefined
const score = firstItem([70, 80]);           // number | undefined
```

TypeScript infers `T` from the argument, so the return type always matches the input. With `any`, both results would lose their types and mistakes would go unnoticed.

## Generics with `Promise<T>`

A `Promise` is itself generic. `Promise<T>` describes a value of type `T` that will be available later, and `await` gives you that `T` back.

```ts
interface User {
  id: number;
  name: string;
}

async function fetchData<T>(url: string): Promise<T> {
  const response = await fetch(url);
  return response.json();
}

const user = await fetchData<User>("/api/v1/users/me");
console.log(user.name); // typed as string
```

Without the generic, `response.json()` returns `any` and every property access is unchecked. With `fetchData<User>`, the editor knows `user` has `id` and `name`. Keep in mind that `T` does not validate data at runtime; it describes the shape you expect the API to return.

## Conclusion

Generics keep code reusable without giving up type safety. Combined with `Promise<T>`, they describe exactly what an asynchronous operation will return, so awaited data is fully typed and errors appear at compile time instead of in production.
