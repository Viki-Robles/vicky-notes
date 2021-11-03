---
title: Apollo Client
tags:
  - graphQl
emoji: 👋
---

### Client Set up

```client.ts
import { GraphQLClient } from 'graphql-request'

const endpoint = `${import.meta.env.VITE_HASURA_ENDPOINT}`
export const graphQlClient = new GraphQLClient(endpoint)
```

### Gql Query Modelling I

```ts
import { QueryKey, useQuery, UseQueryResult } from "react-query";
import { graphQlClient } from "../../graphql/client";

export const useGqlQuery = <ResponseData = unknown, Variables = unknown>(
  queryKey: QueryKey,
  query: string,
  variables?: Variables
): UseQueryResult<ResponseData, Error> => {
  return useQuery(queryKey, async () => {
    try {
      const response = await graphQlClient.request(query, variables);
      return response;
    } catch (error) {
      console.log(`🚀 ~ useGqlQuery ~ error`, error);
    }
  });
};
```

### Gql Query Modelling II

```ts
import {
  QueryKey,
  useQuery,
  UseQueryOptions,
  UseQueryResult,
} from "react-query";
import { auth } from "../../config";
import { graphQlClient } from "../../graphql/client";

/**
 * @name useGqlQuery
 * @description a helper hook that should be used when calling the GraphQL API
 */

export const useGqlQuery = <ResponseData = unknown, Variables = unknown>(
  queryKey: QueryKey,
  query: string,
  variables?: Variables,
  options?: UseQueryOptions<ResponseData, Error, ResponseData, QueryKey>
): UseQueryResult<ResponseData, Error> => {
  return useQuery(
    queryKey,
    async () => {
      try {
        // always get the latest token
        const token = await auth?.currentUser?.getIdToken();

        // if the token is `undefined`, no auth headers will be set
        // this allows us to use the GraphQL API for public queries
        // like the query on the `/talent-spotlight` page
        const authorisationHeaders = token
          ? {
              Authorization: `Bearer ${token}`,
            }
          : undefined;

        const response = await graphQlClient.request(
          query,
          variables,
          authorisationHeaders
        );
        return response;
      } catch (error) {
        console.log(`🚀 ~ useGqlQuery ~ error`, error);
      }
    },
    options
  );
};
```
