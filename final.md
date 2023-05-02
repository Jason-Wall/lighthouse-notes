# Finals Kickoff

- Ask for help - Put your stack in the request.
- Put in the hours - lots of hard work up front and taper down at the end.
- Take breaks and sleep.
- Don't compare to others.
- Be comfortable being uncomforable - focus on learning new things

## Minimum viable demo

- Don't bother with user auth
- Workflow: Idea -> User Stories -> Resources -> ERD -> Routes -> Wireframes
- Schedule last four days for cleanup/ bug squish
- Learning new things means less features.
- Identify your risks - External risks, internal risks. Test your most complex aspects early - have a pivot plan.
-

## Schedule

- Planning through weekend
- Next Week Funcitonal Code through Friday
- Next Week Cleanup/ styling through to Wednesday - dry runs
- Present Thursday

## Tips for personal success

- Try to focus on your weakness
- You should be able to speak to the entire codebase

## Goals for final

- Well design - looks polished. Steal designs if you need to.
- Use modern frameworks - Rails, react, etc.
- After the demo you can tune the product further (login, refactors, testing, etc.)

# Meet with Alvin - Planning

look into multi-page, use session-storage/ local-storage to persist user.
Next does server side rendering. Alternately use react-router - very similar to scheduler-api.

## React Router

`npm i react-router-dom` - Client side

- Can share a link!
- Routes - req.params are handled the same as express - `/products/:productId`
- BrowserRouter is a component. Any child of it benefits froms it's powers. Might be just as well to add it to the \* index.js and wrap <App /> in the BrowserRouter.
- Link is used to update the url. One param - the new url. Lots of params associated with
- Route - Two params the path (url) and the target element to load. Element can be any JSX you like.

in App.js

```js
import './App.css';
import { BrowserRouter, Link, Route } from 'react-router-dom';

import Home from './components/Home';

const App = () => {
  return (
    <div className='App'>
      <h2>React Router Demo</h2>
      <BrowserRouter>
        <Link to='/about'>About</Link>
        <Link to='/'>Home</Link>
        <Link to='/products'>Products</Link>
        <Routes>
          <Route path='/about' element={<About />}></Route>
          <Route path='/' element={<Home />}></Route>
          <Route path='/products' element={<Products />}></Route>
        </Routes>
      </BrowserRouter>
    </div>
  );
};

export default App;
```

## Boiler Plate

[templates](https://hopeful-goodall-ba63af.netlify.app/)

# Project Setup

[Compass - react/ node setup](https://web.compass.lighthouselabs.ca/days/w06d5/activities/1218)
User node v 14 or higher!
`nvm install 16`
`nvm alias default 16`

With one terminal - `npm-run-build`
