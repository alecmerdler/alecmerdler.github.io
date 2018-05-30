# React Using TypeScript and JavaScript

TypeScript has had support for transpiling JSX and JavaScript files for a while, but starting 
to write new components in TypeScript isn't as easy as just adding `.tsx` to your filename.
This post will cover some common pitfalls when migrating an ES6 React codebase to support 
TypeScript.

_button.jsx_
```javascript
import * as React from 'react'

export const CustomButton = (props) => (
    <button className="custom-button" onClick={props.action()}>{props.text}</button>
);
```

_list.tsx_
```typescript
import * as React from 'react';
import { CustomButton } from './button';

export const ListView = (props: ListViewProps) => (
    <div className="">
        <h1>{props.title}</h1>
        <ul>
            {props.items.map(item => (
                <li>
                    <CustomButton title={item.name} action={() => alert(item.name)} />
                </li>
            )}
        </ul>
    </div>
);

export type ListViewProps = {title: string, items: {name: string}[]};
```

_list.spec.tsx_
```typescript
import * as React from 'react';
import { mount, shallow } from 'enzyme';
import { ListView } from './list';

describe('App', () => {
    
    
    it('shallow renders', () => {
        const wrapper = shallow(<ListView />);
    });
    
    it('mounts', () => {
        const wrapper = mount(<ListView />);
    });
});
```
