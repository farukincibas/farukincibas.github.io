---
title: "Material UI Clear Autocomplete Textfield"
date: 2021-09-30T15:34:30-04:00
categories:
  - material-ui
tags:
  - react
  - material-ui
  - autocomplete
---

Last days I realized when I check material ui documentation They did not talk about autocomplete textfield delete process 
that why I want to talk about it how can u delete textfield without click autocomplete cancel mark. maybe you need clear 
autocomplete textfield after some transactions that why I created simple delete function and you can use everywhere.
Today I will use React for explanation.

```ruby
import AutoCompleteExample from '../src/AutoCompleteExample';

function App() {
  return (
    <>
    <AutoCompleteExample></AutoCompleteExample>
    </>
  );
}

export default App;

#=> This is App.js  I defined AutoComplete here first.
```

you need define value and set that value onchange event inside of autocomplete bye the way important thing you must define usestate(null) you can check below code for better understanding.

```ruby
import React, { useState } from 'react';
import TextField from '@mui/material/TextField';
import Autocomplete from '@mui/material/Autocomplete';
import ButtonDelete from './ButtonDelete';


export default function ComboBox() {
    const [valueLabel, setValueLabel] = useState(null);
    return (<>
        <Autocomplete
            disablePortal
            id="autoCompleteExample"
            options={top100Films}
            value={valueLabel}
            onChange={(event, newValue) => {
                if (newValue !== null) {
                    setValueLabel(newValue);
                }
            }}
           
            renderInput={(params) => <TextField {...params} label="Movie" />}
        />
        <br></br>
        <ButtonDelete setValueLabel={setValueLabel}></ButtonDelete>
    </>
    );
}


const top100Films = [
    { label: 'The Shawshank Redemption', year: 1994 },
    { label: 'The Godfather', year: 1972 },
    { label: 'The Godfather: Part II', year: 1974 },
    { label: 'The Dark Knight', year: 2008 },
    { label: '12 Angry Men', year: 1957 },
    { label: "Schindler's List", year: 1993 },
    { label: 'Pulp Fiction', year: 1994 }
];

#=> I called ButtonDelete Component inside of here.
```

now I defined function below and I called with button. that's single line enough for clear autocomplete textfield.

```ruby
import React from 'react';
import Button from '@mui/material/Button';


export default function ButtonDelete({ setValueLabel }) {
    const deleteAutoCompleteTextFieldArea = () => {
        setValueLabel(null);
    }

    return (<>
        <Button onClick={deleteAutoCompleteTextFieldArea} variant="outlined">
            Delete
        </Button></>
    );
}

#=> Now You can find delete function this component.
```


it was my first blog. I will try to make better blogs here. Hope you like it. I am okay for advice so you can achieve me via linkedin.
