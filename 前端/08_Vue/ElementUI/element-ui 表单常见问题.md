## 表单验证规则，清空或填充数据如何避免自动触发
### 场景
使用Element中的form表单检查规则，编辑窗口中填充数据，新建时需重置为初始值：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1039463/1670342451052-31afc316-352b-40af-bb6b-ac84e6507262.png#averageHue=%23fefefe&clientId=ud31c9604-6a18-4&from=paste&id=ua381d20f&name=image.png&originHeight=210&originWidth=1290&originalType=url&ratio=1&rotation=0&showTitle=false&size=40953&status=done&style=stroke&taskId=u7c21b84b-d2b2-4782-b514-1f48299c6b8&title=)
将表单数据进行清空后，出现表单rules规则自动验证提示。
### 解决
方法1：可以使用v-if动态销毁，消耗性能
方法2：使用官网介绍的clearValidate方法（推荐）
```java
// DOM更新后的回调中执行
this.$nextTick(()=>{
    //清除表单内所有规则检测提示
    this.$refs['ruleForm'].clearValidate(); 
    //可清除特定属性
    // this.$refs['ruleForm'].clearValidate('name'); 
 })
```
