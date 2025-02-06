---
tags:
  - React
  - NextJS
  - Axios
  - Redux
---
#### 1. 在需要使用 Redux 的文件中暴露一个 `injectStore` 方法

```ts
// ...
import { toggleAccountModalVisible } from "@/redux/slices/ui";
import { configureStore } from "@reduxjs/toolkit";

type StoreInstance = ReturnType<typeof configureStore>;

let store: StoreInstance;
export const injectStore = (_store: StoreInstance) => {
  store = _store;
};

// 响应拦截器
axiosInstance.interceptors.response.use(
  (response) => {
    // 登录过期
    if (response.data.code === "1001") {
      // 使用 redux
      store.dispatch(toggleAccountModalVisible(true));
    }
    return response.data;
  },
  (err) => {
    return Promise.reject(err);
  },
);

// ...

```
#### 2. 在顶层入口文件中，注入 store

```ts
import React from "react";
import { Provider } from "react-redux";
import { store } from "./store";
import { PersistGate } from "redux-persist/integration/react";
import { persistStore } from "redux-persist";
import PersistLoading from "./persist-loading";
import { injectStore } from "@/request/axios-instance";

// 注入store
injectStore(store);

const ReduxProvider = ({ children }: { children: React.ReactNode }) => {
  return (
    <Provider store={store}>
      <PersistGate loading={<PersistLoading />} persistor={persistStore(store)}>
        {children}
      </PersistGate>
    </Provider>
  );
};

export default ReduxProvider;

```