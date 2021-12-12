---
title: Local Storage
tags:
  - localStorage
emoji: 👋
---

## Step by step Guide to create your own Context and Provider by creating a Favouriting feature

[UselocalStorageState package](https://www.npmjs.com/package/use-local-storage-state)

### Create the initial state

- useContext hook is creating the default/ initial state of

```ts
interface FavouriteProps {
  id: string;
  children: ReactNode;
}

interface FavouriteContextProps {
  isFaved: (id: string) => boolean;
  faves: string[];
  setFavourites: (id) => void;
}

interface UseFavouriteReturn {
  isFaved: (id: string) => boolean;
  setFavourites: (id) => void;
  faves: string[];
}
```

### We create the Context where we initialise the values that we want as we would do with the useState hook, and then we exporting those values so that we can use them to different places

- The way it works is that when we click the favourite button that will add the item to the array. When we click again is gonna remove it. So we initialise the empty array and also we set the state.

- isFaved is a function that returns true if the item we clicked is included in the array.

```ts
const FavouritedContext = React.createContext<FavouriteContextProps>({
  faves: [],
  setFavourites: (doctor_id) => {
    console.log("default setFavourite state");
  },
  isFaved: (doctor_id: string) => {
    return false;
  },
});

export const useFavourite = (): UseFavouriteReturn => {
  const { faves, setFavourites, isFaved } = useContext(FavouritedContext);
  return { faves, setFavourites, isFaved };
};
```

```ts
export const FavouriteProvider = ({
  children,
}: FavouriteProps): JSX.Element => {
  const [faves, setFavourites] = useLocalStorageState<string[]>(
    "favourited-storage",
    []
  );

  const isFaved = (doctor_id: string): boolean => {
    return faves.includes(doctor_id);
  };

  const handdleFavourited = (doctor_id: string): void => {
    const isFavouritedDoctor = isFaved(doctor_id);
    if (!isFavouritedDoctor) {
      const storageFaves = [...faves, doctor_id];
      console.log("faves log", faves);
      setFavourites(storageFaves);
      console.log("setFavourites log", storageFaves);
    } else {
      const indexFavouritedId = faves.indexOf(doctor_id);
      const updatedFaves = faves;
      updatedFaves.splice(indexFavouritedId, 1);
      setFavourites(updatedFaves);
    }
  };
  return (
    <FavouritedContext.Provider
      value={{ isFaved, faves, setFavourites: handdleFavourited }}
    >
      {children}
    </FavouritedContext.Provider>
  );
};
```
