# React-Js

## **Beginner Level (Essential Fundamentals)**

### **Core Concepts**
- **JSX (JavaScript XML)**
  - Syntax and rules
  - Embedding expressions
  - Conditional rendering
  - Lists and keys

##  **What is JSX?**

JSX is a syntax extension for JavaScript that allows you to write HTML-like code directly in your JavaScript files. It's not HTML - it's JavaScript that gets transformed into regular JavaScript function calls.

## 📝 **1. Syntax and Rules**

### **Basic JSX Structure**
```jsx
// ✅ Correct JSX
const element = <h1>Hello, World!</h1>;

// ✅ JSX must be wrapped in a single parent element
const element = (
  <div>
    <h1>Title</h1>
    <p>Paragraph</p>
  </div>
);

// ❌ Wrong - multiple root elements
const element = (
  <h1>Title</h1>
  <p>Paragraph</p>
);
```

### **JSX Rules**
1. **Must return a single element** (use fragments `<>` or `<div>`)
2. **All tags must be closed** (`<img />` not `<img>`)
3. **Use camelCase for attributes** (`className` not `class`)
4. **JavaScript expressions go in curly braces** `{}`

### **Example from your project:**
```jsx
// From your ResetPasswordScreen.jsx
return (
  <Box
    minH="100vh"
    bg={useColorModeValue('gray.50', 'gray.900')}
    py={12}
    px={4}
    sm={6}
    lg={8}
  >
    <Stack spacing={8} mx="auto" maxW="lg" py={12} px={6}>
      {/* Content here */}
    </Stack>
  </Box>
);
```

## 🔤 **2. Embedding Expressions**

JSX allows you to embed any valid JavaScript expression inside curly braces `{}`.

### **Variables and Properties**
```jsx
const name = "John";
const user = { firstName: "Jane", lastName: "Doe" };

const element = (
  <div>
    <h1>Hello, {name}!</h1>
    <p>Welcome {user.firstName} {user.lastName}</p>
    <p>2 + 2 = {2 + 2}</p>
  </div>
);
```

### **Function Calls**
```jsx
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = { firstName: "John", lastName: "Doe" };
const element = <h1>Hello, {formatName(user)}!</h1>;
```

### **Example from your project:**
```jsx
// From your ResetPasswordScreen.jsx
<Heading fontSize="2xl" textAlign="center">
  Reset Password
</Heading>
<Text fontSize="lg" color="gray.600" textAlign="center">
  Enter your new password below
</Text>
```

## 🔀 **3. Conditional Rendering**

JSX supports conditional rendering using JavaScript expressions.

### **Using Ternary Operators**
```jsx
const isLoggedIn = true;

const element = (
  <div>
    {isLoggedIn ? (
      <h1>Welcome back!</h1>
    ) : (
      <h1>Please log in</h1>
    )}
  </div>
);
```

### **Using Logical AND (&&)**
```jsx
const showMessage = true;
const message = "Hello World";

const element = (
  <div>
    {showMessage && <p>{message}</p>}
  </div>
);
```

### **Using if/else statements (outside JSX)**
```jsx
function Greeting({ isLoggedIn }) {
  let content;
  
  if (isLoggedIn) {
    content = <h1>Welcome back!</h1>;
  } else {
    content = <h1>Please log in</h1>;
  }
  
  return <div>{content}</div>;
}
```

### **Example from your project:**
```jsx
// Conditional rendering based on state
{isLoading ? (
  <Spinner size="lg" />
) : (
  <Button
    type="submit"
    colorScheme="blue"
    size="lg"
    fontSize="md"
  >
    Reset Password
  </Button>
)}
```

## 📋 **4. Lists and Keys**

When rendering lists in React, you need to provide a unique `key` prop for each element.

### **Basic List Rendering**
```jsx
const numbers = [1, 2, 3, 4, 5];

const listItems = numbers.map((number) => (
  <li key={number}>{number}</li>
));

const element = <ul>{listItems}</ul>;
```

### **Rendering Objects**
```jsx
const users = [
  { id: 1, name: "John", email: "john@example.com" },
  { id: 2, name: "Jane", email: "jane@example.com" },
  { id: 3, name: "Bob", email: "bob@example.com" }
];

const userList = users.map((user) => (
  <div key={user.id}>
    <h3>{user.name}</h3>
    <p>{user.email}</p>
  </div>
));
```

### **Keys Must Be Unique**
```jsx
// ✅ Good - using unique IDs
const items = [
  { id: 1, text: "Item 1" },
  { id: 2, text: "Item 2" }
];

// ❌ Bad - using array index
const items = ["Item 1", "Item 2"];
const listItems = items.map((item, index) => (
  <li key={index}>{item}</li> // Don't use index as key!
));
```

### **Example from your project context:**
```jsx
// Example of how you might render a list of users
const users = [
  { id: 1, name: "John Doe", role: "Admin" },
  { id: 2, name: "Jane Smith", role: "User" }
];

const UserList = () => {
  return (
    <VStack spacing={4}>
      {users.map((user) => (
        <Box key={user.id} p={4} borderWidth={1} borderRadius="md">
          <Text fontWeight="bold">{user.name}</Text>
          <Text color="gray.600">{user.role}</Text>
        </Box>
      ))}
    </VStack>
  );
};
```

## 🎨 **5. Advanced JSX Patterns**

### **Fragment Syntax**
```jsx
// ✅ Using fragments to avoid extra div
const element = (
  <>
    <h1>Title</h1>
    <p>Paragraph</p>
  </>
);

// ✅ Or with explicit Fragment
import React, { Fragment } from 'react';

const element = (
  <Fragment>
    <h1>Title</h1>
    <p>Paragraph</p>
  </Fragment>
);
```

### **Conditional Classes**
```jsx
const isActive = true;
const isDisabled = false;

const element = (
  <button 
    className={`btn ${isActive ? 'active' : ''} ${isDisabled ? 'disabled' : ''}`}
  >
    Click me
  </button>
);
```

### **Inline Styles**
```jsx
const styles = {
  backgroundColor: 'blue',
  color: 'white',
  padding: '10px'
};

const element = <div style={styles}>Styled content</div>;
```

## 🚀 **6. JSX Best Practices**

### **Keep JSX Clean**
```jsx
// ✅ Good - Extract complex logic
const renderUserInfo = (user) => {
  if (!user) return null;
  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
};

const UserProfile = ({ user }) => (
  <div>
    {renderUserInfo(user)}
  </div>
);

// ❌ Bad - Too much logic in JSX
const UserProfile = ({ user }) => (
  <div>
    {user ? (
      <div>
        <h2>{user.name}</h2>
        <p>{user.email}</p>
      </div>
    ) : null}
  </div>
);
```

### **Use Meaningful Variable Names**
```jsx
// ✅ Good
const userListItems = users.map(user => (
  <UserCard key={user.id} user={user} />
));

// ❌ Bad
const items = users.map(u => (
  <UserCard key={u.id} user={u} />
));
```

## 🔧 **7. Common JSX Mistakes to Avoid**

### **Mistake 1: Forgetting to return JSX**
```jsx
// ❌ Wrong
function Component() {
  const name = "John";
  <h1>Hello {name}</h1>; // Missing return
}

// ✅ Correct
function Component() {
  const name = "John";
  return <h1>Hello {name}</h1>;
}
```

### **Mistake 2: Using reserved words**
```jsx
// ❌ Wrong
<div class="container"> // Should be className

// ✅ Correct
<div className="container">
```

### **Mistake 3: Missing keys in lists**
```jsx
// ❌ Wrong
{items.map(item => <li>{item}</li>)}

// ✅ Correct
{items.map(item => <li key={item.id}>{item}</li>)}
```

JSX is the foundation of React development. Understanding these concepts will help you write cleaner, more maintainable React components. The key is to remember that JSX is just JavaScript with a special syntax that makes it easier to describe what your UI should look like!

- **Components**
  - Functional vs Class components
  - Component composition
  - Props and prop drilling
  - Component lifecycle (Class components)
 

## 🧩 **What are React Components?**

Components are the building blocks of React applications. They are reusable pieces of UI that can contain their own logic, state, and styling.

## ⚡ **1. Functional vs Class Components**

### **Functional Components (Modern Approach)**
Functional components are JavaScript functions that return JSX. They're the preferred way to write components in modern React.

```jsx
// ✅ Functional Component
import React from 'react';

const Welcome = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};

// ✅ With destructuring
const Welcome = ({ name, age }) => {
  return (
    <div>
      <h1>Hello, {name}!</h1>
      <p>You are {age} years old</p>
    </div>
  );
};

// ✅ Arrow function syntax
const Welcome = ({ name }) => <h1>Hello, {name}!</h1>;
```

### **Class Components (Legacy)**
Class components use ES6 classes and have access to lifecycle methods.

```jsx
// Class Component
import React, { Component } from 'react';

class Welcome extends Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}
```

### **Example from your project:**
```jsx
// From your ResetPasswordScreen.jsx - Functional Component
const ResetPasswordScreen = () => {
  const [password, setPassword] = useState('');
  const [confirmPassword, setConfirmPassword] = useState('');
  const [isLoading, setIsLoading] = useState(false);

  return (
    <Box minH="100vh" bg={useColorModeValue('gray.50', 'gray.900')}>
      {/* Component content */}
    </Box>
  );
};
```

## 🎯 **2. Component Composition**

Component composition is the practice of building complex components by combining simpler ones.

### **Basic Composition**
```jsx
// Simple components
const Header = ({ title }) => <h1>{title}</h1>;
const Content = ({ children }) => <main>{children}</main>;
const Footer = () => <footer>© 2024</footer>;

// Composed component
const Page = () => (
  <div>
    <Header title="Welcome" />
    <Content>
      <p>This is the main content</p>
      <p>More content here</p>
    </Content>
    <Footer />
  </div>
);
```

### **Children Prop Pattern**
```jsx
// Container component that accepts children
const Card = ({ children, title }) => (
  <Box borderWidth={1} borderRadius="lg" p={4}>
    {title && <Heading size="md" mb={3}>{title}</Heading>}
    {children}
  </Box>
);

// Usage
const UserProfile = () => (
  <Card title="User Information">
    <Text>Name: John Doe</Text>
    <Text>Email: john@example.com</Text>
  </Card>
);
```

### **Example from your project:**
```jsx
// From your ResetPasswordScreen.jsx - Composition example
const ResetPasswordScreen = () => {
  return (
    <Box minH="100vh" bg={useColorModeValue('gray.50', 'gray.900')}>
      <Stack spacing={8} mx="auto" maxW="lg" py={12} px={6}>
        <Stack align="center">
          <Heading fontSize="2xl" textAlign="center">
            Reset Password
          </Heading>
          <Text fontSize="lg" color="gray.600">
            Enter your new password below
          </Text>
        </Stack>
        <Box rounded="lg" bg={useColorModeValue('white', 'gray.700')} boxShadow="lg" p={8}>
          {/* Form content */}
        </Box>
      </Stack>
    </Box>
  );
};
```

## 📦 **3. Props and Prop Drilling**

### **Props (Properties)**
Props are read-only data passed from parent to child components.

```jsx
// Parent component
const ParentComponent = () => {
  const userData = {
    name: "John Doe",
    email: "john@example.com",
    role: "Admin"
  };

  return <ChildComponent user={userData} isActive={true} />;
};

// Child component
const ChildComponent = ({ user, isActive }) => {
  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.email}</p>
      <span>{isActive ? 'Active' : 'Inactive'}</span>
    </div>
  );
};
```

### **Prop Drilling**
Prop drilling occurs when you pass props through multiple levels of components that don't need them.

```jsx
// ❌ Prop Drilling - Bad Practice
const App = () => {
  const user = { name: "John", email: "john@example.com" };
  
  return (
    <div>
      <Header user={user} />
      <MainContent user={user} />
      <Footer user={user} />
    </div>
  );
};

const Header = ({ user }) => (
  <header>
    <h1>Welcome, {user.name}</h1>
    <Navigation user={user} /> {/* Passing user down */}
  </header>
);

const Navigation = ({ user }) => (
  <nav>
    <UserMenu user={user} /> {/* Passing user down again */}
  </nav>
);

const UserMenu = ({ user }) => (
  <div>
    <span>{user.email}</span> {/* Finally using the user prop */}
  </div>
);
```

### **Solutions to Prop Drilling**

#### **1. Context API**
```jsx
// Create context
const UserContext = React.createContext();

// Provider component
const UserProvider = ({ children }) => {
  const [user, setUser] = useState({ name: "John", email: "john@example.com" });
  
  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
};

// Use context in any component
const UserMenu = () => {
  const { user } = useContext(UserContext);
  
  return <span>{user.email}</span>;
};

// App structure
const App = () => (
  <UserProvider>
    <Header />
    <MainContent />
    <Footer />
  </UserProvider>
);
```

#### **2. Component Composition**
```jsx
// ✅ Better approach using composition
const App = () => {
  const user = { name: "John", email: "john@example.com" };
  
  return (
    <div>
      <Header>
        <UserMenu user={user} />
      </Header>
      <MainContent />
      <Footer />
    </div>
  );
};

const Header = ({ children }) => (
  <header>
    <h1>Welcome</h1>
    <Navigation>{children}</Navigation>
  </header>
);

const Navigation = ({ children }) => (
  <nav>
    {children} {/* Direct access to UserMenu */}
  </nav>
);
```

### **Example from your project:**
```jsx
// Example of props in your ResetPasswordScreen
const ResetPasswordScreen = () => {
  const [password, setPassword] = useState('');
  
  return (
    <PasswordInput 
      value={password}
      onChange={setPassword}
      placeholder="Enter new password"
      isRequired={true}
    />
  );
};

const PasswordInput = ({ value, onChange, placeholder, isRequired }) => (
  <FormControl isRequired={isRequired}>
    <FormLabel>Password</FormLabel>
    <Input
      type="password"
      value={value}
      onChange={(e) => onChange(e.target.value)}
      placeholder={placeholder}
    />
  </FormControl>
);
```

## ⏰ **4. Component Lifecycle (Class Components)**

### **Lifecycle Methods Overview**

```jsx
class LifecycleExample extends Component {
  // 1. Mounting Phase
  constructor(props) {
    super(props);
    this.state = { data: null };
    console.log('1. Constructor called');
  }

  static getDerivedStateFromProps(props, state) {
    console.log('2. getDerivedStateFromProps called');
    return null; // Return new state or null
  }

  componentDidMount() {
    console.log('4. Component mounted');
    // Perfect place for API calls
    this.fetchData();
  }

  // 2. Updating Phase
  shouldComponentUpdate(nextProps, nextState) {
    console.log('5. shouldComponentUpdate called');
    return true; // Return false to prevent re-render
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    console.log('6. getSnapshotBeforeUpdate called');
    return null; // Return snapshot or null
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    console.log('7. Component updated');
    // Handle side effects after update
  }

  // 3. Unmounting Phase
  componentWillUnmount() {
    console.log('8. Component will unmount');
    // Cleanup: cancel API calls, remove event listeners
    this.cancelApiCall();
  }

  // 4. Error Handling
  componentDidCatch(error, errorInfo) {
    console.log('Error caught:', error);
    // Handle errors in child components
  }

  render() {
    console.log('3. Render called');
    return <div>Lifecycle Example</div>;
  }
}
```

### **Detailed Lifecycle Explanation**

#### **Mounting Phase (Component is being created)**
```jsx
class UserProfile extends Component {
  constructor(props) {
    super(props);
    this.state = {
      user: null,
      loading: true
    };
    console.log('Constructor: Component is being created');
  }

  static getDerivedStateFromProps(props, state) {
    // Called before render, can update state based on props
    if (props.userId && !state.user) {
      return { userId: props.userId };
    }
    return null;
  }

  componentDidMount() {
    console.log('ComponentDidMount: Component is now in DOM');
    // Perfect for:
    // - API calls
    // - Setting up subscriptions
    // - Adding event listeners
    this.fetchUserData();
  }

  fetchUserData = async () => {
    try {
      const response = await fetch(`/api/users/${this.state.userId}`);
      const user = await response.json();
      this.setState({ user, loading: false });
    } catch (error) {
      console.error('Error fetching user:', error);
    }
  };

  render() {
    if (this.state.loading) {
      return <div>Loading...</div>;
    }
    return (
      <div>
        <h1>{this.state.user?.name}</h1>
        <p>{this.state.user?.email}</p>
      </div>
    );
  }
}
```

#### **Updating Phase (Component is being re-rendered)**
```jsx
class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  shouldComponentUpdate(nextProps, nextState) {
    // Return false to prevent unnecessary re-renders
    if (nextState.count === this.state.count) {
      return false;
    }
    return true;
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // Called right before the most recently rendered output is committed
    // Useful for capturing information from the DOM
    if (prevState.count < this.state.count) {
      return { message: 'Count increased!' };
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // Called after component updates
    if (snapshot) {
      console.log(snapshot.message);
    }
    
    // Example: Update document title when count changes
    document.title = `Count: ${this.state.count}`;
  }

  increment = () => {
    this.setState(prevState => ({
      count: prevState.count + 1
    }));
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}
```

#### **Unmounting Phase (Component is being removed)**
```jsx
class Timer extends Component {
  constructor(props) {
    super(props);
    this.state = { seconds: 0 };
    this.interval = null;
  }

  componentDidMount() {
    this.interval = setInterval(() => {
      this.setState(prevState => ({
        seconds: prevState.seconds + 1
      }));
    }, 1000);
  }

  componentWillUnmount() {
    // Cleanup: clear the interval
    if (this.interval) {
      clearInterval(this.interval);
    }
    console.log('Timer component unmounted, interval cleared');
  }

  render() {
    return <div>Seconds: {this.state.seconds}</div>;
  }
}
```

### **Error Boundaries**
```jsx
class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI
    return { hasError: true, error };
  }

  componentDidCatch(error, errorInfo) {
    // Log error to an error reporting service
    console.error('Error caught by boundary:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return (
        <div>
          <h1>Something went wrong.</h1>
          <p>{this.state.error?.message}</p>
        </div>
      );
    }

    return this.props.children;
  }
}

// Usage
const App = () => (
  <ErrorBoundary>
    <UserProfile />
  </ErrorBoundary>
);
```

## 🔄 **5. Functional Components with Hooks (Modern Alternative)**

### **Equivalent Lifecycle with Hooks**
```jsx
const UserProfile = ({ userId }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  // componentDidMount equivalent
  useEffect(() => {
    fetchUserData();
  }, []); // Empty dependency array = run once

  // componentDidUpdate equivalent
  useEffect(() => {
    if (userId) {
      fetchUserData();
    }
  }, [userId]); // Run when userId changes

  // componentWillUnmount equivalent
  useEffect(() => {
    return () => {
      // Cleanup function
      console.log('Component will unmount');
    };
  }, []);

  const fetchUserData = async () => {
    try {
      const response = await fetch(`/api/users/${userId}`);
      const userData = await response.json();
      setUser(userData);
      setLoading(false);
    } catch (error) {
      console.error('Error fetching user:', error);
    }
  };

  if (loading) return <div>Loading...</div>;

  return (
    <div>
      <h1>{user?.name}</h1>
      <p>{user?.email}</p>
    </div>
  );
};
```

## 🎯 **6. Best Practices**

### **Component Naming**
```jsx
// ✅ Good - PascalCase for components
const UserProfile = () => {};
const ResetPasswordScreen = () => {};

// ❌ Bad - camelCase or lowercase
const userProfile = () => {};
const resetPasswordScreen = () => {};
```

### **Component Organization**
```jsx
// ✅ Good - One component per file
// UserProfile.jsx
const UserProfile = () => {
  // Component logic
};

export default UserProfile;

// ✅ Good - Related components in same file
// UserComponents.jsx
const UserCard = () => {};
const UserList = () => {};
const UserForm = () => {};

export { UserCard, UserList, UserForm };
```

### **Props Validation**
```jsx
import PropTypes from 'prop-types';

const UserProfile = ({ name, email, age }) => {
  return (
    <div>
      <h1>{name}</h1>
      <p>{email}</p>
      <p>{age}</p>
    </div>
  );
};

UserProfile.propTypes = {
  name: PropTypes.string.isRequired,
  email: PropTypes.string.isRequired,
  age: PropTypes.number
};

UserProfile.defaultProps = {
  age: 18
};
```

Understanding these concepts is crucial for building maintainable React applications. Functional components with hooks are the modern approach, but understanding class components and lifecycle methods is still valuable for working with legacy code or understanding React's evolution!

- **State Management**
  - useState hook
  - State updates and immutability
  - State lifting
  - Local vs global state

- **Event Handling**
  - Synthetic events
  - Event handlers
  - Preventing default behavior
  - Event bubbling and capturing

### **Hooks (React 16.8+)**
- **useState** - Managing component state
- **useEffect** - Side effects and lifecycle
- **useRef** - Accessing DOM elements
- **useCallback** - Memoizing functions
- **useMemo** - Memoizing values
- **useContext** - Sharing data across components

## 🔧 **Intermediate Level**

### **Advanced Hooks**
- **Custom Hooks**
  - Creating reusable logic
  - Hook composition
  - Best practices

- **useReducer** - Complex state logic
- **useLayoutEffect** - Synchronous effects
- **useImperativeHandle** - Exposing imperative methods

### **Performance Optimization**
- **React.memo** - Preventing unnecessary re-renders
- **useMemo and useCallback** - Memoization strategies
- **Code splitting** - Lazy loading components
- **Virtual DOM** - Understanding React's rendering process

### **Routing**
- **React Router**
  - BrowserRouter, Routes, Route
  - Navigation and links
  - Route parameters
  - Nested routes
  - Protected routes

### **Forms and Validation**
- **Controlled vs Uncontrolled components**
- **Form libraries** (Formik, React Hook Form)
- **Validation strategies**
- **Form submission handling**

## 🏗️ **Advanced Level**

### **State Management Libraries**
- **Redux Toolkit**
  - Store setup
  - Slices and reducers
  - Async thunks
  - RTK Query

- **Zustand** - Lightweight state management
- **Context API** - Built-in state sharing
- **Recoil** - Facebook's experimental state management

### **Advanced Patterns**
- **Render Props**
- **Higher-Order Components (HOCs)**
- **Compound Components**
- **Renderless Components**

### **Testing**
- **Jest** - Testing framework
- **React Testing Library**
  - Component testing
  - User interaction testing
  - Accessibility testing
- **Cypress** - E2E testing

### **Performance & Optimization**
- **React DevTools** - Profiling and debugging
- **Bundle analysis** - Webpack Bundle Analyzer
- **Lazy loading** - React.lazy and Suspense
- **Error boundaries** - Error handling

## 🎯 **Specialized Topics**

### **Styling**
- **CSS-in-JS** (Styled Components, Emotion)
- **CSS Modules**
- **Tailwind CSS**
- **Material-UI, Chakra UI** (Component libraries)

### **Data Fetching**
- **Fetch API**
- **Axios**
- **React Query/TanStack Query**
- **SWR**
- **GraphQL with Apollo Client**

### **Build Tools & Development**
- **Create React App**
- **Vite**
- **Webpack configuration**
- **Babel configuration**
- **ESLint and Prettier**

### **Deployment & CI/CD**
- **Netlify, Vercel, AWS**
- **Docker containerization**
- **GitHub Actions**
- **Environment variables**

## 📚 **Recommended Learning Path**

### **Phase 1: Fundamentals (2-3 weeks)**
1. JSX and Components
2. Props and State
3. Event Handling
4. Basic Hooks (useState, useEffect)

### **Phase 2: Intermediate (3-4 weeks)**
1. Advanced Hooks
2. Performance Optimization
3. React Router
4. Forms and Validation

### **Phase 3: Advanced (4-6 weeks)**
1. State Management (Redux Toolkit)
2. Testing
3. Advanced Patterns
4. Performance Optimization

### **Phase 4: Specialization (Ongoing)**
1. Choose a styling solution
2. Learn a data fetching library
3. Master build tools
4. Explore deployment strategies

## 🎯 **Practical Projects to Build**

### **Beginner Projects**
- Todo List App
- Calculator
- Weather App
- Quiz App

### **Intermediate Projects**
- E-commerce Product List
- Blog with CRUD operations
- Dashboard with charts
- Social Media Feed

### **Advanced Projects**
- Full-stack application
- Real-time chat app
- Complex dashboard
- Progressive Web App (PWA)
