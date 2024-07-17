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

