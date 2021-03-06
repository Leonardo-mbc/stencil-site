---
title: Typed Components
description: Typed Components
url: /docs/typed-components
contributors:
  - adamdbradley
  - manucorporat
---

# Typed Components

Web Components generated with stencil come with typing information automatically generated by the Stencil compiler. Typescript declarations provide strong guarantees when consuming components:

- Ensuring that proper values are passed down as properties
- Code autocompletion in modern IDEs such as Atom and VSCode
- Events' details
- Signature of components' methods

This public types are automatically generated by Stencil in `src/component.d.ts`, which allows for strong typing in JSX (just like React) and `HTMLElement` interfaces for each component.

Because Web Components generated by Stencil are just vanilla Web Components, they extend the `HTMLElement` interface. For each component a type named `HTML{CamelCaseTag}Element` is registered at the global scope, meaning developers DO NOT have to import them explicitly, just like `HTMLElement` or `HTMLScriptElement` are not imported.

- `ion-button` => `HTMLIonButtonElement`
- `ion-menu-controller` => `HTMLIonMenuControllerElement`

```tsx
const button: HTMLIonButtonElement = document.queryElement('ion-button');
button.fill = 'outline';
```

**IMPORTANT**: always use the `HTML{}Element` interfaces in order to hold references to components.


## Properties

Component properties and attributes are defined by annotating an instance variable with the
`@Prop()` decorator:

```tsx
@Prop() prop: number;
```

Stencil also **uses the type information** in order to generate the Web Component types and automatically cast the values to the specified type at runtime**:

```tsx
@Prop() str1: string; // string attribute
@Prop() str2: 'md' | 'ios'; // string attribute
@Prop() str3 = 'defaultValue'; // string attribute

@Prop() number1: number; // numeric attribute
@Prop() number2 = 42; // numeric attribute

@Prop() boolean1: boolean; // boolean attribute
@Prop() boolean2 = true; // boolean attribute
```


### Required properties

Using `!` after the variable name, will mark this attribute/property as required, this way the JSX types will ensure
the property is passed out.

```tsx
@Prop() value!: string;
```
