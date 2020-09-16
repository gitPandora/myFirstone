```javascript
for(let i=0;i<5;i++){
    //定义局部变量
}

const num = 1;   //定义常量
```



```javascript
//解构表达式 :解析数组变量
let arr = [2,5,-10,15];

let [,,x,y] = arr;  //结果: x==-10,y==15;    
let [,...rest] = arr;  //结果: rest为[5,-10,15]数组


//解析对象
let person = {name:"jack",age:25}//定义对象
let person2 = {name:"jack",age:24,girl:{name:"rose",age:20}}  //定义嵌套对象

let {name,age} = person;    //结果:   name==jack, age==25
let {name:n} = person;   //结果:  n==jack
let {girl:{name}} = person2;  //结果: name==rose
let {...obj} = person2;  //将person2对象深层拷贝给obj对象, 不是引用赋值obj!=person2
```



```javascript
//函数写法简化
var sum = function(a,b){    //求a+b函数的原本写法
    return a+b;
}

var sum = (a,b) => a+b;    //求a+b的和，类似于lambda表达式，只是在js中用 => 表示箭头




const p = {                 //定义对象
    name:"jack",     
    age: 23,         //对象里面的变量原本写法
    sayhello: function(){     //对象里面的方法 ,也可以写成  sayhello(){console.log("hello");}
        console.log("hello");
    }
}
p.sayhello();    //调用方法打印hello   
```



```javascript
const hello = function(person){         //定义传参函数
     console.log(person.name, person.age);     
}
const p ={name:"jack",age:22};         //定义对象

hello(p);      // 调用函数


//简化,函数传参时解构
const hello = function({name,age}){  console.log(name,age); }
//简化，lambda简化函数定义
const hello = ({name,age}) => console.log(name,age);
```



```javascript
let arr = {'2', '5', '-10', '15', '-20'}    //定义字符串数组
//map对数组做分散处理
let arr2 = arr.map(s => parseInt(s));//s是传入函数的参数，一个参数时不用括号。
                                      //将字符串数组全部转换成int数组

//reduce对数组做聚合处理
arr2.reduce((a,b) => a+b)    //int数组求和。将函数执行结果作为下一次执行函数的第一个参数
```













# vue

​         目前React.js、Vue.js框架较火，angularJS逐渐没落。

​        原本浏览器与js解析引擎一体化。Node.js作为分水岭，将引擎抽取出来，使js可以运行在任何平台，甚至写后端代码。以前前端页面专注页面效果，现在前端服务化，前端独立部署，Node作为前端服务器。	

​       



以前js使用dom操作(document.getElement();)       jQuery封装使dom操作变简单
       现在前端框架使用MVVM架构模式：
          M：model, 模型，数据和一些基本操作
          V：View，视图，页面渲染效果
          VM：View-Model，修改任意一方model与view同步改变，无需开发人员干涉，dom操作完全封装在指令中



安装Node会自带NPM。     NPM中需要引包，国外镜像慢，可以安装nrm工具来切换镜像。  安装完成需重启电脑





Vue生命周期：
             beforeCreate、created：Vue对象属性的注入，监听事件的初始化
			beforeMount、mounted：将Vue代码编译成浏览器可识别的代码并替换源代码
			beforeUpdate、updated：用户改变值，页面重新渲染
			beforeDestroy、destroyed：





### Vue指令：

```javascript
 HTML代码块中写指令标签
     v-on:click="方法名称"      			  绑定事件，
     v-on:keydown="方法名称"	
        自动识别enter键  v-on:keydown.enter="方法名称"
        简写成  @keydown.enter="方法名"
     v-on:submit
        简写成  @submit.prevent					阻止事件
          @mouseover="方法名称"
		  @mouseover.stop="方法名称"

     v-text									将内容都转化成纯文本字符显示
     v-html									将内容中的标签字符解析
     
     
     
     
     
     v-bind:color="mycolor"				只是修饰符，只能用来修饰html标签的属性。
         简写成 :color="mycolor"			  单向绑定，值的获取改为变量。改变一方不会影响另一方
     
     v-model="user.username"		独立拿出来用，从data中取值。将标签的value与data里面的值绑定
     									双向绑定，改变任一方都会影响另一方
     区别见https://www.cnblogs.com/zuoyueer/p/11983781.html
     
     


     
     v-for="(item,index) in arr"			将data里面的arr遍历出来，用{{item}}获取
     
     v-if="flag"						绑定的值为true则显示、false不显示  （  去除dom元素）
     v-show="flag"  			 绑定的值为true则显示、false不显示 （style="display: none"）
     
 script中new Vue({
     el:
     data:{
        
	 },
     methods:{
         方法体
     },
     computed:{
         方法体								HTML标签中可以直接{{方法名}}来引用变量
     },
     watch:{
         方法体（用变量名作为方法名）     深度监控用handler方法 
     }
 });对象
```

​		v-model：双向绑定，同时变化
​		
​    								
​					事件修饰符：
​								.stop   事件冒泡：子类事件向父级传递，也触发父级事件
​								.prevent阻止默认事件

​       v-for：遍历数组

​      

​      v-bind：将HTML原生属性转换成Vue属性，可以动态改变。可以缩写成 : 

​      computed:   计算属性

​     watch: 监控属性（用来监控数据的值，发生变化则触发方法） （深度监控用deep）





### Vue组件：

```javascript
  HTML标签
<script>
    //全局组件，完全独立出来的Vue对象，可以写在任何一个js文件中被引用，所以讲HTML标签包含在对象里面									            	(template)，标签中使用到的参数包含在data()中
    Vue.component("组件id",{       //可以直接以组件id当标签来使用
      template:"HTML标签",
      data(){
          return{ }
      }
  });
    
    
    
    //普通的Vue对象，写在script中，与上方HTML标签绑定
    const app = new Vue({
        el:绑定HTML标签,
        data:{
        }
    });





     //局部组件，就是一个变量，定义出来后需要在Vue对象中引用
      const counter = {
          template:"HTML标签",
          data(){
             return{ }
          }
      }
      
      const app = new Vue({
          el:
          data:{}
          components:{					//用components去引用局部变量
              counter:counter           
          }
      })
</script>

```





### Vue组件间的通信：

```javascript
    父组件向子组件的通信:
    <introduce :title="meg"></introduce>              //2、子组件生成的标签

    <script>
        const introduce = {                          //(局部组件、子组件)，
            template:"<h1>{{title}}</h1>",			//4、组件内部使用该值，并显示
            props:['title']						//3、子组件生成的标签，接受了值，所以需要在组件内
        };											  部定义该属性，才可以接受

        const app = new Vue({                      //1、(父组件)，将值传给HTML标签
            el:"#app",
            data:{ msg:"***********"},
            componets:{ introduce }
        });
    </script>
 			






    子组件向父组件的通信：
         this.$emit('incr');


    同级兄弟间的通信:用vuex插件
```

