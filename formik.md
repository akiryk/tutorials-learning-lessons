# Formik

There are a lot of good resources in the [formik docs](https://formik.org/docs/overview); [this is also a good video series](https://www.youtube.com/playlist?list=PLC3y8-rFHvwiPmFbtzEWjESkqBVDbdgGu). 

See also my Codesandbox test site: https://codesandbox.io/s/formik-learning-qip3w

## Basic setup.
Every input will need:
* `id` -- also, it's conventional to also have a name. 
* `value` is the current value of the input
* `onChange` so the formik.values object remains up to date.
* `onBlur` will keep the formik.touched values up to date
* `onFocus` if you want focus activity

```js
<input
  type="email"
  id="email"
  name="name"
  onChange={formik.handleChange}
  value={formik.values.email}
  onBlur={formik.handleBlur}
/>
```

## Validation
In order to validate,  you need
* has an input has been touched?
* Is the input valid?
* what to display?

To know if input has been touched, add `handleBlur` to the input. This ensures formik will have an accurate `formik.touched` object.

## Reduce boilerplate

`getFieldProps()` will allow us to replace onChange, value, onBlur, and other repeated lines. It requires the name of the form field. 
```js
<input
  type="email"
  id="email"
  { ...formik.getFieldProps("name") }
/>
```

## Formik Components
If you use the Formik context, you can refactor even further with
* Formik
* Form
* Field
* Error
```js
import { Formik, Form, Field, Error } from 'formik';

return (
  <Formik
      initialValues={initialValues}
      validationSchema={validationSchema}
      onSubmit={onSubmit}
    >
      <Form>
        <div className="form-control">
          <label htmlFor="name">Name</label>
          <Field type="text" id="name" name="name" />
          <ErrorMessage name="name" />
        </div>
       // etc
```
