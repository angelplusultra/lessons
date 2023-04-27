# React Hook Form Starter Guide

## Step 1: Install React Hook Form and the DevTools

```bash

npm i react-hook-form 

npm i -D @hookform/devtools


```

## Step 2: Basic Setup

useForm returns an object which contains several properties and methods

- register: a function which returns an object of input properties
- formState: an object containing data about the state of the form (errors, dirty fields)
- handleSubmit: a function used to submit the form
        

```js

import { useForm } from 'react-hook-form'
import { DevTool } from '@hookform/devtools'

export default function App() {
    const form = useForm()
    const onSubmit = (data) => {
    console.log(data);
  };

  return (
    <div className="App">
      <form onSubmit={handleSubmit(onSubmit)} noValidate>
        <input type='email' {...form.register('email')} />
        <input type='username' {...form.register('username')} />
        <input type='password' {...form.register('password')} />
        <button onClick={form.handleSubmit(onSubmit)}>Submit</button>
      </form>
      <DevTool control={control} placement="bottom-right" />
    </div>
  );
}






```


## Step 3: Destructuring the Form Object

```js

import { useForm } from 'react-hook-form'
import { DevTool } from '@hookform/devtools'

export default function App() {
    const { register, handleSubmit } = useForm()
    const onSubmit = (data) => {
    console.log(data);
  };

  return (
    <div className="App">
      <form onSubmit={handleSubmit(onSubmit)} noValidate>
        <input type='email' {...register('email')} />
        <input type='username' {...register('username')} />
        <input type='password' {...register('password')} />
        <button onClick={form.handleSubmit(onSubmit)}>Submit</button>
      </form>
      <DevTool control={control} placement="bottom-right" />
    </div>
  );
}






```

## Step 4: Validation


```js

import { useForm } from 'react-hook-form'
import { DevTool } from '@hookform/devtools'

export default function App() {
    const { register, handleSubmit } = useForm()
    const onSubmit = (data) => {
    console.log(data);
  };

  return (
    <div className="App">
      <form onSubmit={handleSubmit(onSubmit)} noValidate>
        <input type='email' {...register('email', {
                required: {
                        value: true,
                        message: 'Email is required'
                    },
                pattern: {
                        value: /[^@]+@[^\.]+\..+/,
                        message: 'Must be a valid email'
                    }
            })} />
        <input type='username' {...register('username', {
                required: 'Username is required',
                minLength: {
                        value: 8,
                        message: 'Username must be at least 8 characters'
                    }
            })} />
        <input type='password' {...register('password', {
                required: 'Password is required',
                minLength: {
                        value: 8,
                        message: 'Password must be at least 8 characters'
                    },
                maxLength: {
                        value: 20,
                        message: 'Passowrd must be less than 20 characters'
                    },
                validate: (value) => {
                        let valid = false

                        for(const char of value){
                                if(!isNaN(parseInt(char))){
                                        valid = true
                                    }
                            }
                        return valid === true || "Passowrd must include a number"

            })} />
      </form>
      <DevTool control={control} placement="bottom-right" />
    </div>
  );
}






```




the validate property is a custom validation function, it can either be  a single function of an object with multiple methods e.g:
```js
validate:{ 
    hasNumber: (value) => {
        let valid = false

            for(const char of value){
                if(!isNaN(parseInt(char))){
                    valid = true
                }
            }
    return valid === true || "Passowrd must include a number"

    },

}

```







## Step 5: Display Validation Error Messages

```js
export default function App() {
  const { register, handleSubmit, control, formState: { errors } } = useForm();
  const onSubmit = (data) => {
    console.log(data);
  };

  return (
    <div className="App">
      <form noValidate>
      <p>{errors.email?.message}</p>
        <input
          type="email"
          {...register("email", {
            required: {
              value: true,
              message: "Email is required"
            },
            pattern: {
              value: /[^@]+@[^\.]+\..+/,
              message: "Must be a valid email"
            }
          })}
        />
      <p>{errors.username?.message}</p>
        <input
          type="username"
          {...register("username", {
            required: "Username is required",
            minLength: {
              value: 8,
              message: "Username must be at least 8 characters"
            }
          })}
        />
      <p>{errors.username?.password}</p>
        <input
          type="password"
          {...register("password", {
            required: "Password is required",
            minLength: {
              value: 8,
              message: "Password must be at least 8 characters"
            },
            maxLength: {
              value: 20,
              message: "Passowrd must be less than 20 characters"
            },
            validate: (value) => {
              let valid = false;

              for (const char of value) {
                if (!isNaN(parseInt(char))) {
                  valid = true;
                }
              }

              return valid === true || "Password must have a number";
            }
          })}
        />
        <button onClick={handleSubmit(onSubmit)}>Submit</button>
      </form>
      <DevTool control={control} placement="bottom-right" />
    </div>
  );
}
```



Step 6: Yup Integration


First, install the resolvers package from rhf and the yup validation library

```bash

npm i @hookform/resolvers yup

```



```js
import { useForm } from 'react-hook-form'
import { yupResolver } from '@hookform/resolvers/yup'
import * as yup from 'yup'

// Create a schema with yup
const schema = yup.object({
        email: yup.string().email('Must be a valid email').required('Email is required'),
        password: yup.string()
            .required("Password is required")
            .min(4, "Password length should be at least 4 characters")
            .max(12, "Password cannot exceed more than 12 characters"),
        password2: yup.string()
            .required("Confirm Password is required")
            .min(4, "Password length should be at least 4 characters")
            .max(12, "Password cannot exceed more than 12 characters")
            .oneOf([yup.ref("password")], "Passwords do not match")
    })



export default function Form(){
    const { register, handleSubmit } = useForm({
            resolver: yupResolver(schema)
        })

        return (
        <form>
            <p>{errors.email?.message}</p>
            <input {...register('email')} />
            <p>{errors.password?.message}</p>
            <input {...register('password')}/>
            <p>{errors.password2?.message}</p>
            <input {...register('password2')}/>
        </form>
        )
    }

```


