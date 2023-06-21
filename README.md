# React

# Lesson 28
## Can design the parent module directly iside the dependent module
```
const Logitem=(props)=>{
    // props inside the function module's parameter,
    //props point to a object
    //it contains the parent's all transmit parameter.it can trasmit function arrows too.
    console.log(props);
    //-----> {test: '456'}
    console.log(props.desc // props.time)
}
```
```
const Log=()=>{
    return <div className='logs'>
    <Logitem test="456">
    <Logitem date={new Date(2021,10,22,19,0)} desc={'learn react'} time={'50'}>
    </div>
}
```
# Lesson 29
### For the date() module
```
In Logitem class:

const Logitem=(props)=>{
    return(
        <MyDate date={props.date}>
    )
}
const MyDate=(props)=>{
    console.log(props.date.getDate());

    const month =props.date.toLocaleString('zh-CN',{month:'long/numeric'});
    const date =props.date.getDate();

    return(
        <div className='date'>
        <div className='month'>
        april{props.date.getMonth()}// month starts at 0; ---> props.date.toLocaleString('zh-CN',{month:'long/numeric'})
        or
        {month}
        
        </div>
        <div className='day'>
        {date}
        </div>
        </div>
    );
};

export default MyDate;
```

# Lesson 30
props has issues:
```
props.desc = 'hello';<------- **props is read only ,cannot be changed.**
```
**props is from parent transmit data to dependent ,no change allowed.**
The following is not realistic.
```
<Logitem date={new Date(2021,10,22,19,0)} desc={'learn react'} time={'50'}>
```
a set of array data.
```
const logdata=[
    {name:
        id:'01'
        date:new Date(2021,1,20,18,20),
        desc:'new job',
        time:30
    },
        {name:
        id:'02'
        date:new Date(2023,1,22,18,20),
        desc:'leave job',
        time:20
    }
]
 ```

not good. use the index to key that when the order wont changed.
```
const Log=()=>{
    <Logitem date={logdata[0].date desc={logdata[0].desc} time={'logdata[0].time'}>}
 ```

not good enough,using item to represent them
 ```
logdata.map((item,index)=><logitem key={index} date={item.date} desc={item.desc}) time={item.time}
 ```

improved:disconstructed,the attribute should be the same in logitem and item.
 ```
logdata.map(item=><logitem {...item}/>)
 ```

key improved
 ```
    logdata.map((item,index)=><logitem key={index} date={item.date} desc={item.desc} time={item.time}/>)
 ```

the codes are all in jsx ,if codestoo much it will be messy.
 ```
const logitemdate=logdata.map((item,index)=><logitem key={index} date={item.date} desc={item.desc} time={item.time}/>);

return <div className='log'>{
    logitemdate;
}</div>

 ```

# Lesson 31   2023/06/19
 ```
function App () {
  /*
   in react when the module has created or mapped,when you change the variable,it wont changed the module
  */
  let counter = 2

  const addhandle = () => {
    //++
    alert('+1')
    counter++
  }
  const lesshandle = () => {
    //--
    alert('-1')
    counter--
  }
  return <div className='app'>

    <h1>{counter}</h1>
    <button onClick={lesshandle}>-</button>//minus 1 by 1
    <button onClick={addhandle}>+</button>//add 1 by 1
  </div>
}
 ```
# Lesson 32 [state]
Need to rerender.  
**A method that can rerender the module when the variable changes?**
 ```
let counter=2 is useless
 ```
**state is a variable which registered in React and it will monitor the change of this variable,when it changes,it will auto-trigger the rerendering of the Component.**
We use the **hook** to achieve the state
use the **useState()** to create the state
 ```
import{useState} from 'react'
const result=useState(1);
 ```
**console.log(result) will return a matrix as (2)[1,f]**  
the first of the matrix is the initial value ,achieve by **let counter = result[0];**
change the initial value will not trigger the rerendering:
 ```
const result=useState(1);
let counter = result[0];
counter++;
<h1>{counter}</h1>  // useless
 ```


using the second **fn**   to change the state,and trigger the rerendering of the component

```
let setcounter=result[1]
setcounter(counter++)
<h1>{counter}</h1>  // useful
```
**a better way:**
```
const[count,setcount]=useState(1);
```

# Lesson 33 [state code & conditions]
state is a variable being admin by React
-when use setState()to change the value,it will trigger the **rerendering**----> will trigger the diff algo
```
if setCounter(2),it wont rerender it for the second time since its using diff algo which detect that it wont change.
```
update the new object,other attirbute not in it will be discarded
```
const[user,setuser]=useState({name:'tomy',age:18})
setuser({name:'jerry'})
output---> {jerry}
```
if want to change only one value of the object:
```
user.name='jerry'
setuser(user)
```
if change the old state object,the addr still the same,it wont change the result.

**using shallow copy**
```
const newuser=Object.assign({},user)//transfer user values into new empty object{}
newuser.name='jerry';
setUser(newuser);
```
**or a more better way**
```
setUser({...user,name:'jerry'})//the second slot will change the thing in the first slot
```
when using setCounter/setUser,it will change the next counter's value;its **asynchronous**
```
setcounter(1)
setcounter(2)
setcounter(3)
setcounter(4)
```

To avoid if tow trigger are too fast,the result will trigger the diff,then even when 1 click twice it becomes 2 still;
```
const addHandler=()=>{
    settimeout(
        ()={
            setcounter(counter+1)
        },1000
    )
}
```
To avoid this using **Callback**

```
const addHandler=()=>{
    settimeout(
        ()={
            setcounter((prevCounter:number)=>{
                // in setstate()the callback value returns will be the new state value
                // when it execuaes of teh call back,the react will make the new state value to be parameter to transit
                return prevCounter+1; //react ensure it will be the newest
            })
                },1000
    )
}
or 
setCounter(prevState=>prevState+1)
```



