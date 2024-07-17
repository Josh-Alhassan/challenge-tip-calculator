```
import "./App.css"
import { useState } from "react";
```

These two lines import the necessary dependencies. The first line imports CSS styles from a `App.css` file. The scond line imports the `useState` hook from React, which will be used to manage state in the functional components

```
export default function App() {
    return (
        <div>
            <TipCalculator>
        </div>
    )
}
```

This component defines the main `App` component which is exported as the default export. The `App` component returns a JSX element, a `div` containing the `TipCalculator` component.

```
function TipCalculator() {
    const [bill, setBill] = useState("");
    const [percentage1, setPercentage2] = useState("");
    const [percentage2, setPercentage2] = useState("");

    const tip = bill * ((percentage1 + percentage2) / 2 / 100);

    function handleReset() {
        setBill("");
        setPercentage1(0);
        setPercentage2(0);
    }

    return (
        <div>
            <BillInput bill={bill} onSetBill={setBill} />
            <SelectPercentage percentage={percentage1} onSelect={setPercentage1}> How did you like the service?</SelectPercentage>
            <SelectPercentage percentage={percentage2} onSelect={setPercentage2}> How did your friend like the service?</SelectPercentage>

            { bill > 0 && (
                <>
                    <Output bill={bill} tip={tip} />
                    <Reset onReset={handleReset} />
                </>
            )}
        </div>
    )
}
```

The `TipCalculator` component is defined here. Inside this component:
+ Three state variables are defined using the `useState` hook:
    - `bill` to store the bill amount.
    - `percentage` to store the first person'strip percentage.
    - `percentage2` to store the second person's tip percentage.

+ `tip` is a calculated value representing the average tip based on the percentages provided.
+ `handleReset` is a function to reset all state variable to their initial values.
+ The return statement provides the JSX structure for the component:
    - `BillInput` component to input the bill amount.
    - Two `SelectPercentage` components for selecting the tip percentages.
    - if `bill` is greater than 0, it conditionally renders the `output` component to show the calculated tip and the `Reset` component to reset the inputs.

```
function BillInput({ bill, onSetBill }) {
    return (
        <div>
            <label> How much was the bill? </label>
            <input 
                type="text"
                placeholder="Bill Value"
                value={bill}
                onChange={(e) => onSetBill(Number(e.target.value))} 
            />
        </div>
    );
}
```

The `BillInput` component is defined here:
+ It takes `bill` and `onSetBill` as props.
+ It returns a `div` containing a `label` and an `input` element.
+ The `input` element is controlled, meaning its value is set to the `bil` prop, and its `onChange` event updates the `bill` state in the parent component (`TipCalculator`).

```
function SelectPercentage({ children, percentage, onSelect }) {
    return (
        <div>
            <label>{children} </label>
            <select
                value={percentage}
                onChange={(e) => onSelect(Number(e.target.value))}
            >
                <option value="0"> Dissatisfied (0%) </option>
                <option value="0"> Dissatisfied (0%) </option>
        </div>
    )
}
```

The `SelectPercentage` component is defined here:
* It takes `children`, `percentage`, and `onSelect` as props.
* It returns a `div` containing a `label` and a `select` element.
* The `label` displays the `children` prop, allowing for customizable text.
* The `select` element is controlled, with its value set to the `percentage` prop, and its `onChange` event updating the percentage state in the parent component.

```
function Output({bill, tip}) {
    return (
        <h3>
            You pay ${bill + tip} (${bill} + ${tip} tip)
        </h3>
    )
}
```

The `Output` component is defined here:
* It takes `bill` and `tip` as props.
* It returns an `h3` element displaying the total amount to be paid, which is the sim of `bill` and `tip`, and provides a breakdown of the bill and tip amounts.

```
function Reset({ onReset }) {
    return <Button onClick={onReset}>Reset</Button>
}
```

The `Reset` component is defined here:
* It takes `onReset` as a prop.
* It returns a `button` element with an `onClick` event that triggers the `onReset` function passed from the parent component, resting the inputs.