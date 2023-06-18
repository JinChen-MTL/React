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
### For the date() module
```
In Logitem class:

const Logitem=(props)=>{
    return(
        <MyDate date={props.date}>
    )
}
const MyDate=(props)=>{
    return(
        
    )
}


```



