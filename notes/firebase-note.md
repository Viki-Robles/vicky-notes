---
title: Firebase
tags:
  - firebase
  - APIs
emoji: 👋
---

## Firebase Authentication

```ts
// firebase.ts
import firebase from "firebase/app";
import "firebase/auth";
import "firebase/firestore";
import "firebase/functions";

const FIREBASE_CONFIG = {
  apiKey: "{api key}",
  authDomain: "{authDomain}",
  databaseURL: "{databaseURL}",
  projectId: "{app name}",
  storageBucket: "{storageBucket}",
  messagingSenderId: "{messagingSenderId}",
  appId: "{appId}",
  measurementId: "{measurementId}",
};

firebase.initializeApp(FIREBASE_CONFIG);

export const auth = firebase.auth();
export const firestore = firebase.firestore();
export const functions = firebase.app().functions("europe-west2"); // set the region globally

export { firebase };
```
