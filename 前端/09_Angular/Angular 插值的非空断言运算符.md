Angular 非空断言运算符使 TypeScript 类型检查器暂停对特定属性表达式的 null 和 undefined 的严格检查。

`?`用来检查问号前面的变量是否为 null 或者 undefined 时，程序不会出错。

```typescript
stu3: Student;

<h1>stu3 id{{stu3?.id}}</h1>          // stu3 id
<h1>stu3 name{{stu3?.name}}</h1>      // stu3 name
```

比如上面的例子中 stu3 没有初始化，在调用 id 或者 name 的时候，就不会抛出异常。

`!`用来检查感叹号后面的变量为 null 或者 undefined 时，程序不会出错

```typescript
 stu2: Student = {
    id: 1,
    name: undefined,
    age: 3
  };

<h1>stu2 name {{stu2!.name}}</h1>  // stu2 name 
<h1>stu2 id {{stu2!.id}}</h1>            // stu2 id 1
```

上面例子中 stu2 中 name 为 undefined，在调用 stu2.name 时，需要判断下是否为 undefined
