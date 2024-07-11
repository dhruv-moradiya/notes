## 🚀 Redux-Toolkit

1. what is Redux ?

- Redux ek state management library hai jo JavaScript applications mein use hoti hai, especially React ke saath. Yeh ek centralized store provide karti hai jahan humara pura application state store hota hai. Redux ka main concept hai ki application ka state ek single source of truth mein hota hai, aur state changes sirf predictable tarike se hote hain.

- Redux teen main parts pe based hoti hai:

  - Store: Yeh ek object hai jo pura state rakhta hai.
  - Actions: Yeh plain JavaScript objects hote hain jo batate hain ki state mein kya change hona chahiye.
  - Reducers: Yeh functions hote hain jo decide karte hain ki actions ke response mein state kaise update hogi.

- Iska fayda yeh hota hai ki aapke application ka state management predictable aur maintainable hota hai. Aapko easily track kar sakte ho ki kis action ke response mein state kaise change hui hai, aur agar kabhi koi issue hota hai to debug karna relatively easy ho jata hai.

#### Benefits:

      -- Redux Toolkit (RTK) incorporates Immer internally to simplify state updates within reducers. When using RTK's createSlice function, you can write reducers that "mutate" state directly, and RTK will handle the immutability under the hood using Immer.

      -- Immer.js allows you to write simpler and more intuitive code when managing immutable state in Redux. Redux Toolkit leverages Immer internally, so you can directly "mutate" state in reducers created with createSlice, making state management more straightforward and reducing boilerplate code.

- Example ke taur pe, agar aapke paas ek todo list application hai, to Redux aapko help karega track karne mein ki kaunse todos add hue hain, kaunse complete hue hain, aur kaunse delete hue hain, sab kuch ek centralized store mein.

---

2. What is createAsyncThunk in Redux Toolkit?

- Redux Toolkit ka createAsyncThunk ek utility function hai jo asynchronous logic ko handle karna bahut aasan bana deta hai. Jab humein kisi API se data fetch karna hota hai ya koi asynchronous operation perform karna hota hai, tab hum createAsyncThunk use karte hain.

- Suppose karo humein ek user list fetch karni hai kisi API se. Pehle hum Redux mein manually action creators aur thunks likhte the, lekin Redux Toolkit ke createAsyncThunk se yeh kaafi simplified ho gaya hai.

  - createAsyncThunk:

    createAsyncThunk ek function hai jo do parameters leta hai:
    Ek unique string jo action type define karta hai.
    Ek async function jo async logic ko handle karta hai (jaise ki API call).
    Yeh function automatically pending, fulfilled, aur rejected action types create karta hai jo Redux DevTools mein easily traceable hote hain.

- extraReducers:

  extraReducers ke through hum thunks ke alag-alag states ko handle kar sakte hain (pending, fulfilled, rejected).
  pending state mein, hum status ko 'loading' set karte hain.
  fulfilled state mein, hum API se fetched data ko state mein save karte hain.
  rejected state mein, hum error ko handle karte hain.

- Benefits:

  createAsyncThunk asynchronous actions ko manage karna simplified aur organized bana deta hai.
  Thunk ke lifecycle (pending, fulfilled, rejected) automatically handle hoti hai.
  Code readability aur maintainability improve hoti hai, aur less boilerplate code likhna padta hai.

---

3. `createSlice`

`createSlice` Redux Toolkit ka ek function hai jo Redux state aur reducers ko manage karne mein help karta hai. Yeh function state slice create karta hai jisme state, reducers aur actions sab kuch ek saath define kiya jaata hai. Aayiye ise detail mein samjhte hain:

### `createSlice` ka Structure

`createSlice` ek object return karta hai jo kuch is tarah hota hai:

- **name**: Slice ka naam, jo state mein ek key ban jaata hai.
- **initialState**: Initial state jo slice ke liye define hoti hai.
- **reducers**: Reducers jo state ko update karne ke rules define karte hain.
- **actions**: Automatically generated actions based on reducers.

### Example

Chaliye ek example dekhte hain jisme ek counter slice banate hain:

```javascript
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

export default counterSlice.reducer;
```

### Breakdown

1. **name**: `counter` slice ka naam hai.
2. **initialState**: Initial state define karta hai `{ value: 0 }`.
3. **reducers**: Teen reducers define kiye hain:
   - `increment`: State value ko 1 se increment karta hai.
   - `decrement`: State value ko 1 se decrement karta hai.
   - `incrementByAmount`: State value ko action payload ke amount se increment karta hai.

### Actions and Reducers

- `increment`, `decrement`, aur `incrementByAmount` actions ko automatically create kiya jaata hai aur export kiya jaata hai.
- `counterSlice.reducer` ko export kiya jaata hai jo Redux store mein integrate hota hai.

### Usage in Redux Store

Ab is slice ko Redux store mein add karna hoga:

```javascript
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./counterSlice";

const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});

export default store;
```

Is tarah, `createSlice` aapki Redux state management ko simplify karta hai by combining reducers and actions creation in a single step.
