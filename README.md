# Typescript-react-guide
This repo currently only focuses on typescript react. But on the future it will be comprehensive guide on using typescript for developers.
Before consuming this repo I will suggest you to add this config to your `eslint`. Find it [here](https://github.com/aomini/eslint-config-rakeshshrestha)

## Typing React Children
React Children can be typed with these types available on `@types/react`. But they have some key differences that you should know about.

Consider this component:
```tsx
type Props = {
  children: JSX.Element // we will be testing this type
}

const SomeComponent: React.FC<Props> = ({children})=> {
  return <div>
    {children}
  </div>
}
```

### JSX.Element
```tsx
Valid ✅

<SomeComponent>
  <h1>Testing</h1>
</SomeComponent>
```

```tsx
Invalid ❌
🚨 This JSX tag's 'children' prop expects a single child of type 'Element & ReactNode', but multiple children were provided.

<SomeComponent>
  <h1>Testing</h1>
  <h2>here is a star</h2>
</SomeComponent>
```

### JSX.Element[]
```tsx
Valid ✅

<SomeComponent>
  <h1>Testing</h1>
  <h2>here is a star</h2>
</SomeComponent>
```


```tsx
Invalid ❌
🚨 This JSX tag's 'children' prop expects a single child of type 'Element & ReactNode', but multiple children were provided.

<SomeComponent>
  <h1>Testing</h1>
</SomeComponent>
```
_But we can make use of both `JSX.Element` & `JSX.Element[]` to make both the cases valid as._

```tsx
type Props = {
  children: JSX.Element | JSX.Element[]
}
```
### React.ReactChild & React.ReactChild[]
`React.ReactChild` only accepts one component as a children not `jsx` & `React.ReactChild` can accept multiple component as a children.
```tsx
Valid ✅

type Props = {
  children: React.ReactChild | React.ReactChild[]
}

<SomeComponent>
  <Test /> // Where Test is a component
  <Test />
</SomeComponent>
```
```tsx
Invalid ❌
🚨 Cannot accept jsx as a children

<SomeComponent>
  <Test /> // Where Test is a component
  <Test />
  <h1>Testing</h1>
</SomeComponent>
```

### React.ReactNode
Type that rules over all. It accepts everything.
