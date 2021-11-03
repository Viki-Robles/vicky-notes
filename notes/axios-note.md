---
title: Axios
tags:
  - axios
emoji: 👋
---

## Axios Response Object Schema

- data: parsed response body provided by the server
- status: HTTP status code
- statusText: HTTP status message
- headers: HTTP headers (lower case)
- config: the request config that was provided to axios
- request: the last client request instance that generated this response

## Get Data with Axios

```js
axios.get("https://api.github.com/users/mapbox").then((response) => {
  console.log(response.data);
  console.log(response.status);
  console.log(response.statusText);
  console.log(response.headers);
  console.log(response.config);
});
```

## Post Data with Axios I

```js
axios({
  method: "post",
  url: "/login",
  data: {
    firstName: "Finn",
    lastName: "Williams",
  },
});
```

## Post Data with Axios II

```js
axios.post("https://site.com/", {
  name: "Flavio",
});
```

## TypeScript Axios Example

```ts
interface User {
  id: number;
  firstName: string;
}

axios.get<User[]>("http://localhost:8080/admin/users").then((response) => {
  console.log(response.data);
  setUserList(response.data);
});
```

## Sending Custom Headers

```js
const options = {
  headers: { "X-Custom-Header": "value" },
};

axios.post("/save", { a: 10 }, options);
```

### Node.JS query example

```js
const axios = require("axios");

const getBreeds = async () => {
  try {
    return await axios.get("https://dog.ceo/api/breeds/list/all");
  } catch (error) {
    console.error(error);
  }
};

const countBreeds = async () => {
  const breeds = await getBreeds();

  if (breeds.data.message) {
    console.log(`Got ${Object.entries(breeds.data.message).length} breeds`);
  }
};

countBreeds();
```
