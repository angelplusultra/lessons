# React Query Starter Guide

## Step 1: Installation

```
npm i react-query

```

## Step 2: Setting up the Query Client

2.1: You must import the QueryClient class and the QueryClientProvider React Component

2.2: Create an instance of a QueryClient

2.3 Wrap children inside the QueryClientProvider component and pass the queryClient as an argument to the "client" prop, all children of the Provider component will now have accesss to the useQuery hook

```js
// 2.1
import { QueryClient, QueryClientProvider} from 'react-query'

//2.2
const queryClient = new QueryClient()

//2.3
export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Example />
    </QueryClientProvider>
  )
}

```



## Step 3: The useQuery Hook

3.1: Import the useQuery hook
            
3.2: Invoke the useQuery Hook and pass a a config object in as an argument, the config should contain at least the properties of the queryKey and the queryFn

3.3: Destructure desired items from the query object thats returned from the hook 
```js
import { useQuery } from 'react-query'

// SomeChildComponent.jsx
export function Comp(){
  const { data, isLoading, isError, isSuccess, error } = useQuery({
    queryKey: "todos",
    queryFn: fetch("https://jsonplaceholder.typicode.com/todos").then((res) =>
      res.json()
    )
  });


  if (isLoading) {
    return <Spinner />;
  }

  if (isError) {
    return <div>{error.message}</div>;
  }

  return <div>{data.stuff}</div>;
}
  ```

 ## Step 5: What is a Query Key?

  At its core, React Query manages query caching for you based on query keys. Query keys can be as simple as a string, or as complex as an array of many strings and nested objects. As long as the query key is serializable, and unique to the query's data, you can use it!
String-Only Query Keys

The simplest form of a key is actually not an array, but an individual string. When a string query key is passed, it is converted to an array internally with the string as the only item in the query key. This format is useful for:

    Generic List/Index resources
    Non-hierarchical resources

```js

// A list of todos
useQuery('todos', ...) // queryKey === ['todos']

// Something else, whatever!
useQuery('somethingSpecial', ...) // queryKey === ['somethingSpecial']
```
Array Keys

When a query needs more information to uniquely describe its data, you can use an array with a string and any number of serializable objects to describe it. This is useful for:

    Hierarchical or nested resources
        It's common to pass an ID, index, or other primitive to uniquely identify the item
    Queries with additional parameters
        It's common to pass an object of additional options

```js

// An individual todo
useQuery(['todo', 5], ...)
// queryKey === ['todo', 5]

// An individual todo in a "preview" format
useQuery(['todo', 5, { preview: true }], ...)
// queryKey === ['todo', 5, { preview: true }]

// A list of todos that are "done"
useQuery(['todos', { type: 'done' }], ...)
// queryKey === ['todos', { type: 'done' }]

```


## Step 6: Dependant Queries

```js
const { data: user } = useQuery(['user', email], getUserByEmail)

const userId = user?.id

// Then get the user's projects
const { isIdle, data: projects } = useQuery(
  ['projects', userId],
  getProjectsByUser,
  {
    // The query will not execute until the userId exists
    enabled: !!userId,
  }
)

// isIdle will be `true` until `enabled` is true and the query begins to fetch.
// It will the

```

## Step 7: Mutations and the useMutation Hook


The useMutation hook is designed to handle all the create/update/delete requests, when invoked, it returns an object that contains proerties regarding the status of the mutation anda function to trigger the mutation called "mutate()"

```js
function App() {
  const mutation = useMutation(newTodo => {
    return axios.post('/todos', newTodo)
  })

  return (
    <div>
      {mutation.isLoading ? (
        'Adding todo...'
      ) : (
        <>
          {mutation.isError ? (
            <div>An error occurred: {mutation.error.message}</div>
          ) : null}

          {mutation.isSuccess ? <div>Todo added!</div> : null}

          <button
            onClick={() => {
              mutation.mutate({ id: new Date(), title: 'Do Laundry' })
            }}
          >
            Create Todo
          </button>
        </>
      )}
    </div>
  )
}
```

7.1 Import the useMutation Hook

7.2 Invoke the hook, pass in query config, and destructure desired properties and the mutate() function

7.3 When the form is submitted, the mutate function will be invoked and pass an object in as an arg, that object will be passed through the mutationFn in the mutation config which you can use as the body payload of the request or even a query parameter


```js

const {data, isSuccess, isError, mutate, isLoading,  } = useMutation({
mutationKey: 'newTodo',
'mutationFn': (data) => fetch('http://localhost:3000/todos', {
  body: JSON.stringify(data)
}).then(res => res.json())
})


return (

<form onSubmit={(e) => {
    e.preventDefault()
    mutate({id: 1, body: 'Go Shopping', completed: false})
  }}>
  <button>Submit</button>
</form>
  )

```
