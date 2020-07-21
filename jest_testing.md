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
