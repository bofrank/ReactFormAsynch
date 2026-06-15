# ReactFormAsynch

A lightweight React library for handling asynchronous form validation and submission with ease.

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

[Full documentation here]

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## License

MIT
