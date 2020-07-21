# Jest Testing

### Mocking 

```js
import {nameOfModule} from '@mysource/some-utils';

jest.mock('@mysource/some-utils', () => {
  return {
    nameOfModule: jest.fn(),
  };
});

it('gives data back', async () => {
  fetchQuery.mockImplementation(() => {
    return Promise.resolve({
      data: { stuff: { name: 'bill'}},
    });
  });
});

it('gives nothing back', async () => {
  fetchQuery.mockImplementation(() => {
    return Promise.resolve();
  });
});

it('rejects', async () => {
  fetchQuery.mockImplementation(() => {
    return Promise.reject();
  });
});
```
