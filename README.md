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

