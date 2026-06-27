# ReactFormAsynch

A lightweight React library for asynchronous form validation and submission.

## Features

- ⚡ Asynchronous form validation
- 🎯 Simple and intuitive API
- 📦 Lightweight and performant
- ✅ Error handling and display
- 🔄 Support for async operations (API calls, etc.)

## Installation

```bash
npm install react-form-asynch
```

or with yarn:

```bash
yarn add react-form-asynch
```

## Quick Start

```javascript
import { useForm } from 'react-form-asynch';

function MyForm() {
  const { values, errors, handleChange, handleSubmit } = useForm({
    initialValues: {
      email: '',
      password: ''
    },
    onSubmit: async (values) => {
      // Your async submission logic here
      console.log('Submitting:', values);
    }
  });

  return (
    <form onSubmit={handleSubmit}>
      <input
        name="email"
        value={values.email}
        onChange={handleChange}
        placeholder="Email"
      />
      {errors.email && <span>{errors.email}</span>}
      <button type="submit">Submit</button>
    </form>
  );
}
```

## Documentation

ReactFormAsynch provides a single primary hook, useForm, that helps you manage asynchronous form state, validation, and submission in a predictable way.

## useForm
useForm is a custom hook that wires up your form’s values, validation, and submit handler.

```javascript
const {
  values,
  errors,
  handleChange,
  handleSubmit,
  isSubmitting,
} = useForm({
  initialValues,
  validate,
  onSubmit,
});
```

## Parameters
initialValues (object)
An object defining the initial state of your form fields, e.g. { email: '', password: '' }.

validate (optional, function)
A synchronous or asynchronous function that receives values and returns an errors object mapping field names to error messages.

If the returned object is empty, the form is considered valid.

If it contains keys, those messages will be exposed through errors.

onSubmit (async function)
An async function that is called when the form is valid and the user submits.

It receives the current values and is responsible for any side effects such as calling APIs.

## Returned values
values (object)
The current form state keyed by field name.

errors (object)
The current validation errors keyed by field name.

Each property is a string message that you can render next to your inputs.

handleChange (function)
An event handler designed to be passed directly to input components.

It updates values as the user types and optionally triggers validation.

handleSubmit (function)
A function you pass to your <form>’s onSubmit prop.

It will:

Prevent the default browser submit

Run validate (if provided)

Call onSubmit only when the form is valid

Track the isSubmitting state while your async logic runs

isSubmitting (boolean)
Indicates whether an async submission is currently in progress (useful for disabling buttons or showing loading states).

## Example

```javascript
import { useForm } from 'react-form-asynch';

function LoginForm() {
  const {
    values,
    errors,
    handleChange,
    handleSubmit,
    isSubmitting,
  } = useForm({
    initialValues: { email: '', password: '' },
    validate: (values) => {
      const errors: Record<string, string> = {};
      if (!values.email) errors.email = 'Email is required';
      if (!values.password) errors.password = 'Password is required';
      return errors;
    },
    onSubmit: async (values) => {
      // Your async submission logic here (e.g. API call)
      console.log('Submitting:', values);
    },
  });

  return (
    <form onSubmit={handleSubmit}>
      <input
        name="email"
        value={values.email}
        onChange={handleChange}
        placeholder="Email"
      />
      {errors.email && <span>{errors.email}</span>}

      <input
        name="password"
        type="password"
        value={values.password}
        onChange={handleChange}
        placeholder="Password"
      />
      {errors.password && <span>{errors.password}</span>}

      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? 'Submitting…' : 'Submit'}
      </button>
    </form>
  );
}
```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## License

MIT
