# Jest Testing

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
