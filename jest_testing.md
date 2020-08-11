# Jest Testing

### Act Errors

Act errors are telling you that something in your test changed state, and you may be missing things because of it. Kent Dodds has a good article: https://kentcdodds.com/blog/fix-the-not-wrapped-in-act-warning

There are a couple ways to handle it.
1. Use wait-for-expect library
```js
  import waitForExpect from 'wait-for-expect';
  
  it('calls an async function with a new status"', () => {
      const button = wrapper.find('button');
      button.simulate('click');
      // expect one call so far
      expect(myAsyncFunc).toHaveBeenCalledTimes(1);
      return waitForExpect(() => {
        // expect a second call after promise resolves!
        expect(myAsyncFunc).toHaveBeenCalledTimes(2);
        expect(myAsyncFunc).toHaveBeenCalledWith({
          newStatus: "SOME_STATUS"
        });
      });
      // Resolve the promise that is created when calling the toggle function
      // This tells React we expert additional updates, clearing up the "act" warning
      // const promise = Promise.resolve();
      // await act(() => promise);
    });

```

2. Wrap a resolved promise in act.
```js
 it('calls an async function with a new status"', () => {
      const button = wrapper.find('button');
      button.simulate('click');
      // only called once!
      expect(myAsyncFunc).toHaveBeenCalledTimes(1);
      expect(myAsyncFunc).toHaveBeenCalledWith({
        newStatus: "SOME_STATUS"
      });
      // Resolve the promise that is created when calling the toggle function
      // This tells React we expert additional updates, clearing up the "act" warning
      const promise = Promise.resolve();
      await act(() => promise);
      Promise.resolve();
      // Now it's been called twice!
      expect(myAsyncFunc).toHaveBeenCalledTimes(2);
    });
```

### Mocking 

#### Mock React hooks under some circumstances
- This has limited uses, but can help if you want to test a specific part of a component and aren't worried about the hooks

```js
beforeEach(() => {
    jest.spyOn(React, 'useEffect').mockImplementation(f => f());
    jest.spyOn(React, 'useRef').mockImplementation(() => {
      return {current: null};
    });
  });
```

#### Mock a function that helps a component
- put the function in its own file, `helpers.js`
- in your component's test file, import it and mock it just like below. 

```js
import {nameOfModule} from '@mysource/some-utils';

jest.mock('@mysource/some-utils', () => {
  return {
    nameOfModule: jest.fn(),
  };
});

it('gives data back', async () => {
  nameOfModule.mockImplementation(() => {
    return Promise.resolve({
      data: { stuff: { name: 'bill'}},
    });
  });
});

it('gives nothing back', async () => {
  nameOfModule.mockImplementation(() => {
    return Promise.resolve();
  });
});

it('rejects', async () => {
  nameOfModule.mockImplementation(() => {
    return Promise.reject();
  });
});
```
