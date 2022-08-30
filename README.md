# js-interview

Interview Questions
1. Waht is meta programming? How do you achieve in Js?
2. What is generator in js?
3. What is JSONP? How does it work?
4. What is cors? How does it work?
5. What is event loop?
6. What is shadowing?
7. How to create private properties in Js?
8. What will be output for below code?
    ```javascript
    var a = 10;
    (function(){
        console.log(a);
        var a = 20;
        console.log(a);
    })()
   ```
9. What is critical rendering path? (https://developers.google.com/web/fundamentals/performance/critical-rendering-path)
10. What is render tree?
11. What is marcro task and microtask?
12. What will be output for below code?
    ```javascript
         function func1(){
          setTimeout(()=>{
            console.log(x);
            console.log(y);
          },3000);

          var x = 2;
          let y = 12;
        }

        func1();
    ```
13. What will be output for below code?
    ```javascript
    function func2(){
      for(var i = 0; i < 3; i++){
        setTimeout(()=> console.log(i),2000);
    }

    }

    func2();
    ```
 14. What will be output for below code?
     ```javascript
        let x= {}, y = {name:"Ronny"},z = {name:"John"};
        x[y] = {name:"Vivek"};
        x[z] = {name:"Akki"};
        console.log(x[y]);
     ```
 15. Given a string find out unique words and number of times occured in the string (sentence).
    e.g: 
```javascript 
// input : 'it is a blue moon light and the quick brown fox jumps over the lazy dog. The lazy dog, ran in the moon light along with the brown fox';
// output: it=1, is=1, a =1, blue=1, moon=2, light=2, and=1, the=5, quick=1, brown=2, fox=2, jumps =1, over=1, lazy=2, dog=2, ran=1 in = 1, along=1, with=1
```
  
# interviews

## Get address from any one of the object of the array with destructuring.

```javascript
var users = [
  { name: 'x', address: { pincode: '123' } },
  { name: 'y', address: { pincode: '1234' } },
];
```

## Solution

```javascript
const [userOne] = users;
const { address } = userOne;
const { pincode } = address;
```

## Question

```javascript
let temp = [
  {
    type: 'ULCER',
    prob: 20,
  },
  {
    type: 'DIAB',
    prob: 10,
  },
  {
    type: 'BP',
    prob: 30,
  },
];
```

```javascript
let output = [
  {
    subType: 'ULCER',
    prob: 20,
  },
  {
    subType: 'DIAB',
    prob: 10,
  },
  {
    subType: 'BP',
    prob: 30,
  },
];
```

## Solutions

`javascript const actualOutput = temp.map(({type, ...rest})=>({...rest, subType: type}));`

## Merge below array of objects based on age.

```javascript
var input1 = [
  { name: 'nisum', office: 'kondapur1', age: 10 },
  { name: 'nisum', office: 'kondapur2', age: 20 },
  { name: 'nisum', office: 'kondapur3', age: 40 },
  { name: 'nisum', office: 'kondapur4', age: 5 },
  { name: 'nisum', office: 'kondapur5', age: 1 },
];
```

```javascript
var input2 = [
  { location: 'hyderabad50', age: 50 },
  { location: 'hyderabad10', age: 10 },
  { location: 'hyderabad20', age: 20 },
  { location: 'hyderabad40', age: 40 },
  { location: 'hyderabad5', age: 5 },
  { location: 'hyderabad1', age: 1 },
];
```

```javascript
var output = [
  { name: 'nisum', office: 'kondapur5', age: 1, location: 'hyderabad1' },
  { name: 'nisum', office: 'kondapur4', age: 5, location: 'hyderabad5' },
  { name: 'nisum', office: 'kondapur1', age: 10, location: 'hyderabad10' },
  { name: 'nisum', office: 'kondapur2', age: 20, location: 'hyderabad20' },
  { name: 'nisum', office: 'kondapur3', age: 40, location: 'hyderabad40' },
  { location: 'hyderabad50', age: 50 },
];
```

## Solutions

```javascript
const mergeTwoArrays = (arr1, arr2, key) => {
  const map = {};
  [...arr1, ...arr2].forEach((ele) => {
    if (map[ele[key]]) {
      map[ele[key]] = { ...map[ele[key]], ...ele };
    } else {
      map[ele[key]] = { ...ele };
    }
  });
  return Object.values(map);
};
```


```
/**
1. How can you change the drop down values for days using react when the month and year is updated. 
Note :- Need to consider for leap year that has 29 days for February month
2. How can you calculate the day of the week (Mon,Tue,Wed,..) 
with the assumption of 01/01/2000 is Saturday. 
Note :- Need to consider for leap year that has February month with 29 days
 */

import React, { useEffect, useState } from "react";
import ReactDOM from "react-dom";
import "./styles.css";
 
const dayNames = ['Saturday', 'Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'];
const months = [
  { text: "January", days: 31 },
  { text: "February", days: 28 }, // 29 days if leap year
  { text: "March", days: 31 },
  { text: "April", days: 30 },
  { text: "May", days: 31 },
  { text: "June", days: 30 },
  { text: "July", days: 31 },
  { text: "August", days: 31 },
  { text: "September", days: 30 },
  { text: "October", days: 31 },
  { text: "November", days: 30 },
  { text: "December", days: 31 }
];

const ToDoApp = () => {
  const [dayOfWeek, setDayOfWeek] = useState("");
  const [year, setYear]= useState(2000);
  const [month, setMonth]= useState(months[0].text);
  const [days, setDays]= useState(months[0].days);
  const [isLeap, setLeap]= useState(months[0].days);
  const [day, setDay]= useState(1);

  useEffect(()=>{
    const monthObj = months.find(({text})=>text===month)
    const extraDay = (year%4 === 0 && month === 'February' ? 1: 0);
    setLeap(!!extraDay);
    setDays(monthObj.days+extraDay);
  },[year, month])

  const getYears = () => {
    let opt = [];
    for (let i = 2000; i <= 2050; i++) {
      opt.push(
        <option value={i} key={i}>
          {i}
        </option>
      );
    }
    return opt;
  };

  const getDays = (range=31) => {
    let opt = [];
    for (let i = 1; i <= range; i++) {
      opt.push(
        <option value={i} key={i}>
          {i}
        </option>
      );
    }
    return opt;
  };

  const getDayOfWeek = () => {
    
    const daysFromYear = (year-2000)*365; 

    let accumulatedLeapDays=0;
    for (let i = 2000; i < year; i++) {
      if(i%4 === 0){
        accumulatedLeapDays++;
      }
    }

    let monthIndex;
    let daysOfMonth;

    months.find(({text, days}, index)=>{
      if(text === month) { 
        monthIndex=index+1;
        daysOfMonth = days;
        return true
      }else{
        return false
      }});

    const daysFromMonth = (monthIndex-1)*(daysOfMonth);
    const daysFromDay = day-1;
    const totalDays = daysFromDay + daysFromMonth + daysFromYear + accumulatedLeapDays;
    const _dayOfWeek = totalDays%7;
    setDayOfWeek(dayNames[_dayOfWeek]);
  };

const changeMonth = (event)=>{
  setMonth(event.target.value)
}
const changeYear  = (event)=>{
  setYear(event.target.value);
}
const changeDay = (event)=>{
  setDay(event.target.value);
}

  return (
    <div>
      <h2>Year</h2>
      <select name="years" id="years" onChange={changeYear}>
        {getYears()}
      </select>
      <h2>Month</h2>
      <select name="month" id="month" onChange={changeMonth}>
        {months.map((item) => (
          <option value={item.text} key={item.text}>
            {item.text}
          </option>
        ))}
      </select>
      <h2>Day</h2>
      <select name="day" id="day" onChange={changeDay}>
        {getDays(days)}
      </select>
      <p>
        <button onClick={getDayOfWeek}>Submit</button>
      </p>
      <p className="outLabel">{dayOfWeek}</p>
    </div>
  );
};
ReactDOM.render(<ToDoApp />, document.getElementById("root"));

```
