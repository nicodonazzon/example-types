# example-types

Ejemplos de tipos de datos que se pueden encontrar en typescript

**Estructuras de datos:**

- `Array<T>`:
```typescript
const numbers: number[] = [1, 2, 3, 4, 5];
const names: string[] = ["Alice", "Bob", "Charlie"];
```

- `Tuple`:
```typescript
let person: [string, number] = ["Alice", 30];
person = ["Bob", 25];
```

- `Map<K, V>`:
```typescript
const ages = new Map<string, number>();
ages.set("Alice", 30);
ages.set("Bob", 25);

console.log(ages.get("Alice")); // 30
console.log(ages.get("Bob")); // 25
```

- `Set<T>`:
```typescript
const uniqueNumbers = new Set<number>();
uniqueNumbers.add(1);
uniqueNumbers.add(2);
uniqueNumbers.add(3);
uniqueNumbers.add(2); // Ignorará el valor duplicado

console.log(uniqueNumbers); // Set { 1, 2, 3 }
```

- `WeakMap<K, V>`:
```typescript
let obj1 = {};
let obj2 = {};
const weakMap = new WeakMap();
weakMap.set(obj1, "valor 1");
weakMap.set(obj2, "valor 2");

console.log(weakMap.get(obj1)); // "valor 1"
console.log(weakMap.get(obj2)); // "valor 2"

obj1 = null; // Perderá la referencia
console.log(weakMap.get(obj1)); // undefined
```

- `WeakSet<T>`:
```typescript
let obj1 = {};
let obj2 = {};
const weakSet = new WeakSet();
weakSet.add(obj1);
weakSet.add(obj2);

console.log(weakSet.has(obj1)); // true
console.log(weakSet.has(obj2)); // true

obj1 = null; // Perderá la referencia
console.log(weakSet.has(obj1)); // false
```

**Funciones y objetos relacionados:**

- `Function`:
```typescript
const sum: Function = (a: number, b: number) => {
  return a + b;
};

console.log(sum(2, 3)); // 5
```

- `Date`:
```typescript
const now: Date = new Date();
console.log(now); // Muestra la fecha y hora actual
```

- `RegExp`:
```typescript
const pattern: RegExp = /[A-Za-z]+/;
console.log(pattern.test("Hello")); // true
console.log(pattern.test("123")); // false
```

- `Error`:
```typescript
try {
  throw new Error("Este es un mensaje de error");
} catch (e: Error) {
  console.error(e.message); // "Este es un mensaje de error"
}
```

- `Promise<T>`:
```typescript
function fetchData(): Promise<string> {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Datos obtenidos");
    }, 2000);
  });
}

fetchData().then((data) => {
  console.log(data); // "Datos obtenidos" (después de 2 segundos)
});
```

- `Iterable<T>`:
```typescript
const numbers: Iterable<number> = [1, 2, 3, 4, 5];

for (const num of numbers) {
  console.log(num);
}
```

- `Iterator<T>`:
```typescript
const numbers: number[] = [1, 2, 3, 4

, 5];
const iterator: Iterator<number> = numbers[Symbol.iterator]();

console.log(iterator.next().value); // 1
console.log(iterator.next().value); // 2
console.log(iterator.next().value); // 3
```

¡Por supuesto! Aquí tienes ejemplos de uso de cada uno de los tipos adicionales mencionados en TypeScript:

- `any`: representa cualquier tipo de valor.
```typescript
let variable: any = 10;
variable = "Hola";
variable = true;
```

- `void`: indica la ausencia de un valor.
```typescript
function logMessage(): void {
  console.log("Este es un mensaje.");
}

const result: void = logMessage();
console.log(result); // undefined
```

- `never`: representa un tipo de valor que nunca ocurre.
```typescript
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {
    console.log("Bucle infinito.");
  }
}

// En ambos casos, las funciones nunca retornan un valor o finalizan.
```

- `unknown`: representa un valor desconocido.
```typescript
let userInput: unknown;
let userName: string;

userInput = "Hola";
if (typeof userInput === "string") {
  userName = userInput; // Se realiza una verificación de tipo antes de asignar a otro tipo
}
```

- `this`: representa el tipo "this" en un contexto de objeto.
```typescript
class MyClass {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  greet(): void {
    console.log(`Hola, soy ${this.name}.`);
  }
}

const obj = new MyClass("Alice");
obj.greet();
```

- `Partial<T>`: convierte todos los miembros de un tipo `T` en opcionales.
```typescript
interface Person {
  name: string;
  age: number;
}

const partialPerson: Partial<Person> = {};
partialPerson.name = "Alice";
partialPerson.age = 30;
```

- `Required<T>`: convierte todos los miembros opcionales de un tipo `T` en obligatorios.
```typescript
interface Options {
  name?: string;
  age?: number;
}

const requiredOptions: Required<Options> = {
  name: "Alice",
  age: 30
};
```

- `Readonly<T>`: convierte todos los miembros de un tipo `T` en solo lectura.
```typescript
interface Point {
  readonly x: number;
  readonly y: number;
}

const point: Readonly<Point> = { x: 10, y: 20 };
point.x = 30; // Error: No se puede asignar a una propiedad de solo lectura
```

- `Pick<T, K>`: selecciona un subconjunto de propiedades del tipo `T` especificadas por las claves (`K`).
```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

const personNameAndAge: Pick<Person, "name" | "age"> = {
  name: "Alice",
  age: 30
};
```

- `Record<K, T>`: crea un objeto con claves (`K`) y valores (`T`).
```typescript
type Fruit = "Apple" | "Banana" | "Orange";
type Price = number;

const fruitPrices: Record<Fruit, Price> = {
  Apple: 1.0,
  Banana: 0.5,
  Orange: 0.8
};
```

- `Exclude<T, U>`: excluye los tipos de `U` de `T`.
```typescript
type Numbers = 1 | 2 | 3 | 4 | 5;
type ExcludeTwoThree = Exclude<Numbers, 2 | 3>;

const num

: ExcludeTwoThree = 1; // Solo se puede asignar 1, 4 o 5
```

- `Omit<T, K>`: omite las propiedades del tipo `T` especificadas por las claves (`K`).
```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

const personWithoutAge: Omit<Person, "age"> = {
  name: "Alice",
  address: "123 Main St"
};
```

- `NonNullable<T>`: excluye `null` y `undefined` de `T`.
```typescript
let value: string | null | undefined = "Hello";
const nonNullableValue: NonNullable<typeof value> = value; // Elimina null y undefined
```

¡Espero que estos ejemplos te ayuden a comprender mejor cómo utilizar estos tipos en TypeScript!
