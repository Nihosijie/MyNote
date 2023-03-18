1.可选链运算符 ?.
是不是经常遇到这样的错误: 
TypeError : Cannot read properties of null (reading 'xxx')

引入可选链就是为了解决这个问题 ~~

        const person = { id: 1, name: '李明', desc: null };
 
        // 你可能会这样做
        console.log(person.desc.age) // TypeError 
        console.log(person.desc && person.desc.age); // null
 
        // 使用可选链
        console.log(person.desc?.age); // undefined
        // 或深度可选链
        console.log(person.desc?.address?.city); // undefined
        // 函数可选链
        console.log(person.fun?.());//undefined
2.空值合并运算符 ??

 在左侧值为 null 或 undefined  时，使用右侧的值

        const person = { id: 1, name: '李明', desc: null };
 
        // 当左侧的值存在时
        console.log(person.id ?? person.name);
 
        // 当左侧值为null时
        console.log(person.desc ?? person.name);
        // 当左侧值为undefined
        console.log(person.skill ?? person.name);
3.逻辑空赋值运算符  ??= 

在左侧值为 null 或 undefined  时，对其赋值

        const person = { id: 1, name: '羊乐多', desc: null };
 
        // 当左侧的值存在时
        console.log(person.id ??= person.name);// 1
 
        // 当左侧值为null时
        console.log(person.desc ??= '羊乐多多多多');
        // 当左侧值为undefined
        console.log(person.skill ??= '羊乐多多多多');
		
	```js
	
	```
	