---
id: version-2.0.0-hook-example-use-context
title: useContext Hook
sidebar_label: useContext Hook
original_id: hook-example-use-context
---

```javascript
import React, { createContext, useContext } from 'react';

import { renderHook } from '../../';

test('should get default value from context', () => {
  const TestContext = createContext('foo');

  const { result } = renderHook(() => useContext(TestContext));

  const value = result.current;

  expect(value).toBe('foo');
});

test('should get value from context provider', () => {
  const TestContext = createContext('foo');

  const wrapper = ({ children }) => (
    <TestContext.Provider value="bar">{children}</TestContext.Provider>
  );

  const { result } = renderHook(() => useContext(TestContext), { wrapper });

  expect(result.current).toBe('bar');
});

test('should update value in context', () => {
  const TestContext = createContext('foo');

  const value = { current: 'bar' };

  const wrapper = ({ children }) => (
    <TestContext.Provider value={value.current}>{children}</TestContext.Provider>
  );

  const { result, rerender } = renderHook(() => useContext(TestContext), { wrapper });

  value.current = 'baz';

  rerender();

  expect(result.current).toBe('baz');
});
```