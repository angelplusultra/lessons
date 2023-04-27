# Axios Starter Guide

## Step 1: Install Axios

```bash
npm i axios
```

## Step 2: Basic Usage

```js
import axios from 'axios'

//axios requests can be made a few different ways, one way is by calling any of the request methods (get(), put(), post(), delete(), patch() etc..)

// Notice how compared to the Fetch API, Axios abstracts the need to call the json() method to format the request to access the data payload
axios
  .get("https://jsonplaceholder.typicode.com/todos/1")
  .then((response) => console.log(response))
  .catch((err) => console.log(err));


  // Optional options object for third argument
axios
  .get("https://jsonplaceholder.typicode.com/todos/1", {
          headers: {
            Authorization: 'Bearer SOMETOKEN'  
        }
      })
  .then((response) => console.log(response))
  .catch((err) => console.log(err));

```



## Step 3: Sending Data in Body (Post/Put/Patch/Delete Requests)

```js
// Notice how with axios we dont need to JSON.stringify() our body object before sending
axios
  .post("https://jsonplaceholder.typicode.com/todos/1", {
          body: {
            username: 'gary',
            password: 'abc123'
    }
      })
  .then((response) => console.log(response))
  .catch((err) => console.log(err));


```


## Step 4: Axios Instances

The create() method allows us to make a reusable request config 


```js
const api = axios.create({
        baseUrl: 'https://jsonplaceholder.typicode.com',
        headers: {
            'Authorization': 'Bearer TOKEN'
        }
    }) 

api.get('/todos')
.then(res => console.log(res))
.catch(err => console.log(err))
```
