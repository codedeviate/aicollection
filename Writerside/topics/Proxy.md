# Proxy

A JavaScript Proxy is a powerful concept in JavaScript that allows you to create a transparent wrapper around an object or a value. It enables you to intercept and modify the behavior of an object, allowing for advanced features such as dynamic property handling, data transformation, and caching.

## What is a Proxy?

In JavaScript, a Proxy is an object that acts as a middleman between another object and an application. It receives requests from the application, checks if they should be allowed, and then either allows them to pass through or modifies their behavior before sending them back to the application.

## Why Use Proxies?

Proxies are useful for a variety of purposes, including:

* **Dynamic property handling**: Proxies can be used to create dynamic properties on an object, allowing you to add or remove properties at runtime.
* **Data transformation**: Proxies can be used to transform data as it is being accessed, such as converting dates to different formats or performing calculations.
* **Caching**: Proxies can be used to cache frequently accessed data, reducing the number of requests made to a server.
* **Validation and sanitization**: Proxies can be used to validate and sanitize user input, ensuring that it conforms to certain rules or expectations.

## Creating a Proxy

There are several ways to create a proxy in JavaScript:

### Using the `Proxy` Constructor

This is the most common method of creating a proxy.

```javascript
const target = {};
const handler = {
  get(target, prop) {
    return 'Hello, world!';
  },
};

const proxy = new Proxy(target, handler);
```

### Using the `Proxy` Trap Methods

There are several methods that can be used to create and configure a proxy, including `get`, `set`, `has`, and `deleteProperty`.

```javascript
const target = {};
const handler = {
  get() {
    return 'Hello, world!';
  },
};

Object.create(target, handler);
```

## Proxy Traps

There are several traps that can be used to configure a proxy:

* **get**: This trap is called when an object property is accessed.
* **set**: This trap is called when an object property is set.
* **has**: This trap is called when the `in` operator is used on an object.
* **deleteProperty**: This trap is called when the `deleteProperty` method is used on an object.

## Example Use Case

Here's an example of how you might use a proxy to create a read-only version of an object:

```javascript
const originalObject = {
  name: 'John Doe',
  age: 30,
};

const readOnlyProxy = new Proxy(originalObject, {
  get(target, prop) {
    return target[prop];
  },
});

console.log(readOnlyProxy.name); // "John Doe"
console.log(readOnlyProxy.age); // 30
try {
  readOnlyProxy.name = 'Jane Doe';
} catch (error) {
  console.error('Cannot modify property of read-only proxy');
}
```

In this example, the `get` trap is used to intercept access to the `name` and `age` properties, returning their values directly. The `set` trap is not defined, so attempting to set a new value for either property will throw an error.