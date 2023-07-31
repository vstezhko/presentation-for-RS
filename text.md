# React Query

---

## What is React Query?

- a library designed for React applications

---

## What does React Query do?

- simplifies fetching, caching, and updating data.

---

## Querying data with React Query

----

1) Define a function to fetch your data.
```
  const fetchData = async () => {
  const response = await fetch('https://api.example.com/data');
  if (!response.ok) {
    throw new Error('Failed to fetch data');
  }
  return response.json();
};
```

----


2) Use the useQuery hook to query the data in your component:

```
  function DataDisplay() {
  const { data, isLoading, error } = useQuery('data', fetchData);

  if (isLoading) {
    return <div>Loading...</div>;
  }

  if (error) {
    return <div>Error: {error.message}</div>;
  }

  return (
    <div>
      <h2>Data:</h2>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}
```

---

## Mutations and Updating Data

----

1) Define a function to perform the mutation. This could be an API call to update data on the server:

```
  const updateData = async (updatedData) => {
  const response = await fetch('https://api.example.com/update', {
    method: 'PUT',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(updatedData),
  });

  if (!response.ok) {
    throw new Error('Failed to update data');
  }

  return response.json();
};
```

----

2) Use the useMutation hook to perform the mutation in your component:

```
function DataUpdater() {
  const queryClient = useQueryClient();
  const mutation = useMutation(updateData, {
    onSuccess: (data) => {
      queryClient.invalidateQueries('data');
    },
  });

  const handleUpdate = () => {
    mutation.mutate({ id: 1, name: 'Updated Data' });
  };

  return (
    <div>
      <button onClick={handleUpdate}>Update Data</button>
      {mutation.isLoading && <div>Updating...</div>}
      {mutation.isError && <div>Error: {mutation.error.message}</div>}
      {mutation.isSuccess && <div>Data Updated Successfully!</div>}
    </div>
  );
}
```

---

## Performance and optimizations

----

 - <span style="color: lightblue"><u>Intelligent Caching</u></span> – automatically caches fetched data, reducing the number of requests to the server and improving the overall performance of your application.

----

 - <span style="color: lightblue"><u>Background Fetching</u></span> – performs background fetching to keep data up-to-date, minimizing the impact on user experience and ensuring fresh data is always available.

----

 - <span style="color: lightblue"><u>Automatic Retries</u></span> – automatically retries failed requests, providing a more robust and resilient data-fetching experience.

----

 - <span style="color: lightblue"><u>Query Invalidation and Refetching</u></span> – allows developers to easily invalidate and refetch queries when data changes, ensuring the application always displays the latest information.

---

 official documentation https://tanstack.com/



