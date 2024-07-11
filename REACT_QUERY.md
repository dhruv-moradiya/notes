# 🚀 REACT-QUERY

## 👉 React Query mein kuch important states

1. Fresh:

- Fresh state tab hoti hai jab aapka data abhi-abhi fetch kiya gaya ho aur bilkul up-to-date ho.
- Jab aapne data ko abhi abhi fetch kiya hai aur woh latest hai, tab woh fresh state mein hota hai.

2. Fetching:

- Fetching state tab hoti hai jab aapka data currently server se fetch ho raha hota hai.
- Jab aap kisi API se data fetch kar rahe hote ho aur woh process chal raha hota hai, tab aapka data fetching state mein hota hai.

3. Paused

- Paused state tab hoti hai jab aapka data fetching kisi reason se temporarily ruk gaya ho, lekin resume ho sakta hai.
- Agar aapka internet connection weak hai aur fetching process temporarily stop ho gaya hai, to woh paused state mein hoga.

4. Stale:

- Stale state tab hoti hai jab aapka data fetch ho chuka hota hai lekin ab woh outdated ho gaya hai aur usko update karne ki zarurat hai.
- Agar aapka data ek certain time ke baad update nahi hua hai, to React Query usko stale mark kar deta hai, aur aapko batata hai ki ab is data ko dobara fetch karna chahiye.

5. Inactive:

- Inactive state tab hoti hai jab aapka query abhi active nahi hai, yaani aapne use karna band kar diya hai.
- Agar aapka component unmount ho gaya hai aur ab usko data fetching ki zarurat nahi hai, to query inactive state mein chali jaati hai.

## 😍😍\_**\_----\_\_**----\_**\_----\_\_**----\_**\_----\_\_**----\_\_\_\_----

## 👉 useMutation hook

- React Query ka useMutation hook kaafi powerful tool hai jo mutations ko handle karne ke liye use hota hai. Mutations ka matlab hota hai data ko create, update, ya delete karna. useMutation ka use karke hum easily in operations ko perform kar sakte hain aur apne application ko jyada interactive bana sakte hain. Chalo, isko detail me samajhte hain.

## 😁 Example

- Ek example ke through samjhte hain. Man lo, hume ek user ko add karna hai:

  ```js
  import { useMutation } from "react-query";
  import axios from "axios";

  const addUser = async (newUser) => {
    const response = await axios.post("/api/users", newUser);
    return response.data;
  };

  const MyComponent = () => {
    const mutation = useMutation(addUser);

    const handleAddUser = () => {
      mutation.mutate({ name: "John Doe", age: 30 });
    };

    return (
      <div>
        <button onClick={handleAddUser}>Add User</button>
        {mutation.isLoading ? (
          <p>Loading...</p>
        ) : mutation.isError ? (
          <p>Error occurred: {mutation.error.message}</p>
        ) : (
          mutation.isSuccess && <p>User added successfully!</p>
        )}
      </div>
    );
  };
  ```

## Explanation:

1. Importing and Mutation Function:

- `useMutation` ko import karte hain.
  `addUser` function ko define karte hain jo backend API ko call karta hai.

2. Using useMutation Hook:

- `useMutation` hook ko call karte hain aur addUser function ko pass karte hain.
- `mutation` object ko return karta hai jo various properties aur methods ko hold karta hai jaise `mutate`, `isLoading`, `isError`, `isSuccess`, etc.

3. Handling User Addition:

- `handleAddUser` function ko define karte hain jo `mutation.mutate` ko call karta hai aur naya user data pass karta hai.
- Button click par `handleAddUser` call hota hai.

4. UI Feedback:

- `mutation.isLoading` true hone par "Loading..." message show hota hai.
- `mutation.isError` true hone par error message show hota hai.
- `mutation.isSuccess` true hone par success message show hota hai.

## 😍😍\_**\_----\_\_**----\_**\_----\_\_**----\_**\_----\_\_**----\_\_\_\_----

## 👉 data ko invalidate karna

- React Query mein "data ko invalidate karna" ka matlab hai ki aap React Query ko ye batate hain ki current data outdated ho gaya hai aur usko dobara fetch karne ki zarurat hai. Iska use tab hota hai jab aap data update karte hain, add karte hain ya delete karte hain aur chahte hain ki latest data ko server se fetch kiya jaye.

## 😁 Example:

- Maan lo aapke paas ek todo list application hai jismein aap todos ko add, update aur delete kar sakte hain. Jab aap ek naya todo add karte hain, to aap chahenge ki todo list ka data fresh ho jaye aur usmein latest todo include ho. Iske liye aap data ko invalidate kar sakte hain taaki React Query ko pata chale ki usko list dobara fetch karni hai.

1. Step : React Query Setup:

- Aapke paas query key aur fetch function hona chahiye jo data ko fetch karta hai.

  ```js
  import { useQuery } from "@tanstack/react-query";

  const fetchTodos = async () => {
    const response = await fetch("/api/todos");
    return response.json();
  };

  const { data, error, isLoading } = useQuery("todos", fetchTodos);
  ```

2. Step : Data Invalidation:

- Jab aap data mutate (add, update, delete) karte hain, to aap invalidateQueries method use karte hain taaki React Query ko pata chale ki data ko dobara fetch karna hai.

  ```js
  import { useMutation, useQueryClient } from "@tanstack/react-query";

  const addTodo = async (newTodo) => {
    const response = await fetch("/api/todos", {
      method: "POST",
      body: JSON.stringify(newTodo),
      headers: {
        "Content-Type": "application/json",
      },
    });
    return response.json();
  };

  const MyComponent = () => {
    const queryClient = useQueryClient();
    const mutation = useMutation(addTodo, {
      onSuccess: () => {
        // Invalidate and refetch
        queryClient.invalidateQueries("todos");
      },
    });

    const handleAddTodo = () => {
      const newTodo = { title: "New Todo" };
      mutation.mutate(newTodo);
    };

    return <button onClick={handleAddTodo}>Add Todo</button>;
  };
  ```

  ## 😁 Summary:

- Data Invalidate Karna:

  - Matlab React Query ko bolna ki current data purana ho gaya hai aur naya data fetch karna hai.

- Kab Use Karein:

  - Jab aap data add, update ya delete karte hain aur chahte hain ki latest changes reflect ho.

- Kaise Karein:

  - useQueryClient hook ka use karke invalidateQueries method ko call karen, jismein aap query key pass karte hain.
