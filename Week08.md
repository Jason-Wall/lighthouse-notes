## Full Stack Summary w Andy

- Start a react app.
- npm init -y
- npm Install your faves - express, morgan
- Create a git

### Backend

- build server - require express, etc. start server and test in browser/postman.
- middleware - bodyparsers - urlencoded, json, etc.
- db - In memory or database (need to require pg, etc.)
- create CRUD endpoints - test using [postman](postman.com).
- setup CORS for frontend work.

### Frontend - React

- Where does state live? highest common parent. pass down as props.
- useState (state, setState)
- Clear out react garbage.
- npm start, lets see index.html
- Create components, starting from the leaves and working to the root. Test along the way.
- SASS if you like. `npm i sass` then convert all css files to scss.
- axios to make get/posts. useEffect for first requests or special requests.

## Cross Origin Resource Sharing

We are using one port for our front end and another for back...\
Need to permit other origins.\
`npm install cors`
See documentation, can setup specific endpoints to be permitted.\
Alternately, add a proxy in backend package.json.
`"proxy": "http://localhost:XXXX"`, switch all gets to relative paths.

## Express Static

`app.use(express.static('public'))`
Static files are automatically served when a user routes to `/`. Good for index.html, scripts, css... etc.\
When using react we have to source to build instead of public.

## Testing

### Prop types

[prop-types](https://legacy.reactjs.org/docs/typechecking-with-proptypes.html#proptypes) is a quick and dirty test that can be written directly into the code to check props. Similar to how typescript or flow works.\
`npm install --save-dev prop-types`

## Testing React

We can break a unit test into three phases.

1. Initialize the component that we would like to test.
2. Trigger the change that executes the unit.
3. Verify that the unit produced the expected result.

[Jest](https://jestjs.io/) will test any js, jsx, ts, tsx with the following scheme:

- `src/components/__tests__/Button.js`
- `src/components/Button.test.js`
- `src/components/Button.spec.js`

[Jest matchers](https://jestjs.io/docs/expect)\
[Jest DOM mathcers](https://github.com/testing-library/jest-dom)\
[React Testing Library](https://testing-library.com/docs/react-testing-library/intro)
