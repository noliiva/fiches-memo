source : Samuel Resua (https://medium.com/@samuelresua/global-state-machine-with-react-context-afd0d5475592)
# App.js
```javascript
import ReactDOM from 'react-dom';
import Store from './store';

const App = () => (
  <Store>
    ...
  </Store>
);

ReactDOM.render(<App />, document.getElementById('root'));
```

# store/index.js
```javascript
import createStore from './createStore';
import counter from './counter';
import toggle from './toggle';

const { Store, ...contexts } = createStore([counter, toggle]);

export contexts;
export default Store;
```

# store/contextExample.js
```javascript
const contextExample = {
  name: 'Example',
  initialState: {
    param: 'pouet',
  },
  reducer: (state, action) => {
    switch (action.type) {
      case 'actionType':
        // Update state
        const newState = {
          ...state, 
          params: action.payload,
        };
        return newState;
        
      default:
        return state;
    }
  },
}

export default contextExample;
```

# store/createStore.js
```javascript
const createStore = (config = []) => {
  // Reduce into an object of providers and context
  const { contexts, providers } = config.reduce(
    (acc, { name, initialState, reducer }) => {
      // Context
      const stateContext = React.createContext();
      const dispatchContext = React.createContext();

      // Create provider
      const Provider = ({ children }) => {
        const [state, dispatch] = React.useReducer(reducer, initialState);
        
        return (
          <State.Provider value={state}>
            <Dispatch.Provider value={dispatch}>{children}</Dispatch.Provider>
          </State.Provider>
        )
      }

      // Set and return
      acc.providers.push(<Provider />);
      acc.context[name] = { state: stateContext, dispatch: dispatchContext };
      
      return acc;
    },
    {
      providers: [],
      contexts: {},
    }
  )

  // Create store
  const Store = ({ children: initial }) =>
    providers.reduce(
      (children, parent) => React.cloneElement(parent, { children }),
      initial
    );

  return { Store, ...contexts };
}

export default createStore;
```

# components/ComponentExample.js
```javascript
import { Example } from '../store';

const ComponentExample = () => {
  const { param } = React.useContext(Example.state);
  const dispatch = React.useContext(Example.dispatch);
  
  const handleClick = () => {dispatch('actionType', { payload: 'pouik' })};

  return (
    <div>
      <p>Context param: {param}</p>
      <button onClick={handleClick} >Click me</button>
    </div>
  );
}

export default ComponentExample;
```
