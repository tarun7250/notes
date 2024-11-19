

# types of testing
unit integration, end to end

## unit testing 
- focuses on testing individual blocks - functions, classes, testing is done in isolation, 
- dependencies are mocked 
- jest, `npm install jest` `yarn add -D jest`
- two environments called node and jsdom
- Test cases contain assertions that check
- Test files are usually placed in a directory named \__tests__ and suffixed with .spec.ts
- test suites, which are logical groupings of related test cases, through describe function
- getBy, findBy, queryBy,
```js

```
- jest is a test runner finds, runs, tell whether tests passed or failed
- react testing library provides a virtual dom for testing, core testing library is dom testing library, rtl is wrapper around this
- 

## integration test
- testing combination of units ensuring working together
- 

## end to end test 
- testing entire application flow
- real ui , real backend, real serivces...
-  


# test(name: string, function: ()=>ret, timeout:number) test/it
- name identifier
- function - contains expectations to test
- how long wait bfore aborting the test
```tsx
import { render, screen } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  render(<App />); //renders component
  const linkElement = screen.getByText(/learn react/i);//finds the element case(lower/upper) dependent
  expect(linkElement).toBeInTheDocument();//expect(element).toBeIntheDocument();
});
```
- test.only -> only to run this test -> fit
- test.skip -> skips to run this test -> xit

# describe("",()=>{}) // can have multiple tests
- nestable under describe

```tsx
describe("test suite", ()=> {
    testfunc1("name1",()=>{},t1)
    testfunc2("name2",()=>{},t2)
})
```

# coverage
- how much code is covered during testing
- statements - how many statements
- line - how many lines
- branches - how many conditional branches (if/switch)
- function - how many function
- how many uncovered lines
- `yarn test` checkes only changed files from last commit
- `yarn test --coverage` 
- `yarn test --coverage --watchAll` run all test and then gives coverage report
- `--collectCoverageFrom = 'src/components/**/*.{ts,tsx}"`  to cover only these files in coverage or test
- `--collectCoverageFrom = '!src/components/**/*.{types,constants,test,spec}.{ts,tsx}"`  to cover only these files in coverage or test
```json
"jest": {
    "coverageThreshold": {
        "global": {
            "branches": 80,
            "functions": 80,
            "lines": 80,
            "statements": -10//more than 10 uncovered
        }
    }
}
```

## assertions
- decides whether test passes or fails
-  with jest  expect method carries this
- `expect(value)` with some matcher function
- matcher list = `https://jestjs.io/docs/using-matchers`
- `github.com/testing-library/jest-dom`

## filename convention
- file with .js or .tsx under \_\_test__
- .test.tsx / .test.js
- .spec.tsx / .spec.js

## rtl queries
- render the component
- find element rendered by the component
- assert against the element found, which will pass or fail the test
- getBy.. getAllBy..
- queryBy.. queryAllBy..
- findBy.. findAllBy..
- .. can be Role, LableText, PlaceholderText, Text, DisplayValue, AltText, Title, TestId

## getBy..
- get by query and if none or more than 1 then error
- getByRole - get by aria role
- testing-library.com/docs/queries
```js
getByRole("role", {
    name: (label of form/ text content /arial-label)
})
```
- gets the input by label
```js
screen.getByLabelText('Name');
screen.getByLabelText('Name',{
    selector: 'input'//html tagname
});
```
- get by placeholder
```js
screen.getByPlaceholderText('placeholder');
```
- `getByText`
- searches for all the elements having text node with textContent matching the given text
```js
screen.getByText("str",{
    exact:false,//case insensitive and also searches for substr
})
screen.getByText(regex);
screen.getByText((content)=?bool);
```
- getByDisplayValue
```js
```

- priority order - getByRole > getByLabelText > getByPlaceholderText > getByText > getByDisplayValue > getByAltText > getByTitle > getByTestId 

- getAllBy - returns array of elements which matches the given query
- 
`toHaveLength`

## queryBy
- if multiple then error, if 1 then gives if 0 then null
- all by, gives array  -> if 0 then empty array
- 
## findBy
- returns promise checks after 1 second default if  1 found resolved if multiple or no found rejected then error thrown
- all -> return array if 0 then error
- third optional parameter `{timeout: 1000}`
- 
## screen.debug()
- prints dom structure at a given time

## logRoles()
- logs all the roles
```js
const view = Render(<Component/>);
logRoles(view.container);
```

# user-event
- `import userEvent from 'rtl'`
- convenience API
- `await userEvent.click(element)`
- `dbClick()`, `tripleClick()`, `hover()`, `unHover()`
- pointer apis
- `pointer({keys: '[MouseLeft]'}, target: element)`
- `pointer({keys: '[MouseLeft>]'}, target: element)` click pressed
- `pointer({keys: '[/MouseLeft]'}, target: element)` click released

### typing in input field
- `await userEvent.type(elemtment, "text")`
- `expect(elemtment).toHaveValue("text")`;

### tabbing
- `await userEvent.tab()`
- `expect(element).toBeFocus()` 

type is utility api 
and tab is convenience api
clear()
selectOptions()
deselectOptions()
expect(element.selected).toBe(false);
upload()

clipboardapi
cut()
copy()
paste()

## keyboard api
- keyboard('foo')
- keyboard('{Shift>}a{/Shift}');


## provider wrapped components and custom hooks
- wrapper can be added above the component
```js
test(" ", () => {
    render(<Component/>, {
        wrapper: AppProviders,
    })
    const element = getByText("text");
    expect(element).toHaveTextContent("text");
})
```

## making custom render function 

```js
const customRender = (ui, options) => render(ui, {
    wrapper:AppProviders,
    ...options,
})
export * from "@testing-library/react"
export {customRender as render};
```

## renderHook function to test hooks
```js
const result = renderHook(hookName, {
    initialProps: {
        initialCount: 10; 
    }
})
expect(result.current.count).toBe(10);
```
use act function for state updates what it does is applies the state updates and then check the assertions

```js
act(()=> result.current.handleIncrement());
  expect(result.current.count).toBe(6);
```

## mocks
- Mock is a simulated or fake version of a module, function, or object that is used during testing. 

```js

const mockFunction = jest.fn();

render(<Component handleClick = "mockFunction"/>);
const element = screen.getByText("text");
await user.click(elementButton);
expect(mockFunction).toHaveBeenCalledTimes(1)

```



## spyons
- `spyFn.mockReturnValue(args)` -> `expect(spyFun).toBe(returnValue)`
- `spyFn.mockImplementation`


### mocking http requests
- msw





context mock providers 