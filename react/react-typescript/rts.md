# React TypeScript

## Step 1: Typing Props

The props object of a component needs an explicit type definition

It can be defined with either type or interface

```js
type UserCardProps = {
        id: number
        username: string
        profilePic: string
        isVerified: boolean
    }
export function UserCard({id, username, profilePic, isVerified}: UserCardProps){


        return (<>
        <h3>{username}</h3>
        <img src={profilePic} />
        {isVerified && <BlueCheckmark />}
        </>)
    }

```

## Step 2: Typing useState Hook

TypeScript will infer the type by its initial value, however if it were to change types, you would need to explicitly specify the type witha generic 
```js
const [count, setCount] = useState(0)



type User = {
name: string
id: number
}
const [user, setUser] = useState<User | null>(null)

setUser({
name: 'Mac',
id: 5,
})

```
You can also use Type Assertion


```js

const [cart, setCart] = useState([] as CartType)

```



## Step 3: Typing the Event Object

Inline handlers will correctly type the event automatically
```js
<button onClick={(e) => console.log(e)}>Submit</button>

```

Handlers defined outside will have to explicitly typed

```js
// Form change event
const handleChange = (e: React.ChangeEvent<HTMLFormElement>) => {}


const handleSubmit = (e: React.MouseEvent<HTMLButtonElement>) => {}

```


## Step 4: Typing the "children" Prop

```js

export function Provider({children}: {children: React.ReactNode}){

return (
{children}
)
}


```


## Step 5: Typing Context

Here we are typing what the "value" of the context will be when we pass it into the provider
```js

import { createContext } from "react";

type ThemeContextType = {
        theme: 'light' | 'dark'
        setTheme?: React.Dispatch<React.SetStateAction<"light" | "dark">>
    }

const ThemeContext = createContext<ThemeContextType>({
        theme: 'light',
    });

```

```js
import { useState } from "react";

const App = () => {
  const [theme, setTheme] = useState<ThemeContextType>("light");

  return (
    <ThemeContext.Provider value={{theme, setTheme}}>
      <MyComponent />
    </ThemeContext.Provider>
  );
};

```
## Bonus: List of common typing situations
```js
type AppProps = {
  message: string;
  count: number;
  disabled: boolean;
  /** array of a type! */
  names: string[];
  /** string literals to specify exact string values, with a union type to join them together */
  status: "waiting" | "success";
  /** an object with known properties (but could have more at runtime) */
  obj: {
    id: string;
    title: string;
  };
  /** array of objects! (common) */
  objArr: {
    id: string;
    title: string;
  }[];
  /** any non-primitive value - can't access any properties (NOT COMMON but useful as placeholder) */
  obj2: object;
  /** an interface with no required properties - (NOT COMMON, except for things like `React.Component<{}, State>`) */
  obj3: {};
  /** a dict object with any number of properties of the same type */
  dict1: {
    [key: string]: MyTypeHere;
  };
  dict2: Record<string, MyTypeHere>; // equivalent to dict1
  /** function that doesn't take or return anything (VERY COMMON) */
  onClick: () => void;
  /** function with named prop (VERY COMMON) */
  onChange: (id: number) => void;
  /** function type syntax that takes an event (VERY COMMON) */
  onChange: (event: React.ChangeEvent<HTMLInputElement>) => void;
  /** alternative function type syntax that takes an event (VERY COMMON) */
  onClick(event: React.MouseEvent<HTMLButtonElement>): void;
  /** any function as long as you don't invoke it (not recommended) */
  onSomething: Function;
  /** an optional prop (VERY COMMON!) */
  optional?: OptionalType;
  /** when passing down the state setter function returned by `useState` to a child component. `number` is an example, swap out with whatever the type of your state */
  setState: React.Dispatch<React.SetStateAction<number>>;
};

```
