
## 前端开发编码规范

> 基础规范推荐 [Eslint-standard](#https://github.com/standard/standard)标准, 该规范为补充 `Eslint` 之外的编码标准.


### 目录:

- [项目文件管理规范](#p1)
- [HTML编码规范](#p2)
- [CSS规范](#p3)
- [JS规范](#p4)
- [React编码规范](#p5)
- [项目分支管理规范](#p6)
- [其它](#p6)


### <h3 id='p1'>项目文件管理规范</h3>
1. 目录管理   

```code
Project
    |- src
        |- 业务代码目录
    |- scripts
        |- 脚本文件目录
    |- assets
        |- 编译代码目录
    |- public
        |- 公共资源文件目录
    |- config
        |- 项目相关配置文件目录
    |- doc
        |- 项目文档目录
    |- .gitignore
    |- package.json
    |- README.md
```
2. 项目文件命名规范
    - 目录统一小写命名
    - 文件名采用 `-` 连接, 如: `user-name.js`
    
    
### <h3 id='p2'>HTML编码规范</h3>
1. 语义化标签   
尽量遵循HTML标准和语义，但是不应该以浪费实用性作为代价；
任何时候都要用尽量小的复杂度来解决问题。
2. 减少标签数量   
在编写HTML代码时，需要尽量避免多余的父节点.
3. 属性顺序  
推荐使用下面的属性顺序:   
    - class
    - id
    - name
    - data-*
    - src, for, type, href, value , max-length, max, min, pattern
    - placeholder, title, alt
    - aria-*, role
    - required, readonly, disabled
2. 外部资源引用省略协议名, 如 `src='//xxx.com/image.png'`
    

### <h3 id='p3'>CSS编码规范</h3>
1. 命名规范
    * 常规ID和类名避免使用大写命名, 采用中划线连字符方式, 如 `.home-header`
    * 推荐 `BEM` 规范
2. 样式规范
    * 样式顺序推荐： 
        1. 结构性属性:   
        display   
        position, left, top, right etc.   
        overflow, float, clear etc.   
        margin, padding    
        2. 表现性属性：  
        background, border etc.  
        font, text    
        3. 其它.  
        4. 推荐使用`css combo`插件自动维护属性顺序.
        
    * 对于复用度较高的属性, 采用定义局部或全局变量的方式.
    * 嵌套层级不宜过多. 以最多4层为宜.  
    * 避免使用 `important`.

### <h3 id='p4'>JS编码规范</h3>
1. 命名
    - 标准变量采用驼峰式命名.
    - 常量全大写，用下划线连接.
    - `localStorage/sessionStorage`   
        - 持久数据以 `$$name` 命名
        - 本地会产生修改的暂存数据以 `__name` 命名
        - 合理配置命名空间, 如: `__home_name`, `$$agent_date`
1. 空行

    以下几种情况需要空行：
    - 变量声明后（当变量声明在代码块的最后一行时，则无需空行）
    - 注释前（当注释在代码块的第一行时，则无需空行）
    - 代码块后（在函数调用、数组、对象中则无需空行）
    - 文件最后保留一个空行

2. 注释

    下面情况下要求注释:
    
    - 难于理解的代码段
    - 可能存在错误的代码段
    - 浏览器/语言特殊的HACK代码
    - 业务逻辑强相关的代码
3. 函数
    - 单个函数代码行数不能过多.
    - 单个函数实现的功能不能过多, 保持函数的功能单一性, 适当提取单功能函数.
    
### <h3 id='p5'>React编码规范</h3>   

#### 基础规范
- 统一全部采用 Es6
- 组件文件名称采用大驼峰命名
- 组件文件使用一致的.js或 .jsx后缀, 不得混用.
- Stateless(Function)组件 优先于 Es6 Class；
- 推荐使用 `prop-types`
- key: 不能使用数组 index ，构造或使用唯一的 id
- 每一个文件以 `export default` 的形式暴露一个组件。
- 每个存放组件的目录使用一个index.js以命名导出的形式暴露所有组件。
允许一个文件中存在多个不同的组件，但仅允许通过export default暴露一个组件，其它组件均定义为内部组件。
- 在适当的情况下优化`shouldComponentUpdate`. 
- 生命周期按下面的顺序原则保持 :
    - static
    - constructor
    - getChildContext
    - componentWillMount
    - componentDidMount
    - componentWillReceiveProps
    - shouldComponentUpdate
    - componentWillUpdate
    - componentDidUpdate
    - componentWillUnmount
    - render
    - customeFunction ...

#### 组件规范
- 避免在容器组件 `render` 内部处理大量业务逻辑, 应当将逻辑划分到各组件内部处理. 
- 使用onXxx形式作为props中用于回调的属性名称。
- 使用isXxx形式作为props中用于描述状态的属性名称。
- 对于所有非isRequired的属性，在defaultProps中声明对应的值。   
   - 声明初始值有助于对组件初始状态的理解，也可以减少propTypes对类型进行校验产生的开销。   
   - 对于初始没有值的属性，应当声明初始值为null而非undefined。
   - 对于没有初始化默认值的变量, 使用时需校验数据合法性. 如: `list && list.map()`
- 容器组件:

```
const defaultProps = {
  name: 'Guest'
};
const propTypes = {
  name: React.PropTypes.string
};
class Person extends React.Component {

  // 构造函数
  constructor (props) {
    super(props);
    // 定义 state
    this.state = { smiling: false };
    // 定义 eventHandler
    this.handleClick = this.handleClick.bind(this);
  }

  // 生命周期方法
  componentWillMount () {},
  componentDidMount () {},
  componentWillReceiveProps () {}
  componentWillUnmount () {},

  // getters and setters
  get attr() {}

  // handlers
  handleClick() {},

  // render
  renderChild() {},
  render () {},

}

/**
 * 类变量定义
 */
Person.defaultProps = defaultProps;

/**
 * 统一都要定义 propTypes
 */
Person.propTypes = propTypes;
```
- 无状态组件

```
const Person = ({ name, age }) => {
    const title = name + age
    return (
        <div>
            {title}
        </div>
    )
}
```


#### 注释
- 页面主更新逻辑中针对不同的逻辑补充说明注释:

```
componentWillReceiveProps (nextProps) {
    if (xxx) {
        // 提交处理后的处理回调.
        this.deal()
    }
}
```
    
- 定义的自定义方法如果命名不能直观描述方法功能, 需补充方法注释.
- 其它需要注释的地方. 

#### JSX规范

-  组件用法

```
// 对于多属性需要换行，从第一个属性开始，每个属性一行。
<Foo
    superLongParam="bar"
    anotherSuperLongParam="baz"
/>

<Foo superLongParam="bar" anotherSuperLongParam="baz" />
```

```
render() {
  return (
    <MyComponent className="long body" foo="bar">
      <MyChild />
    </MyComponent>
  );
}
```

- JSX属性
    - 组件样式优先在 `css` 文件中编写. `style` 属性不宜超过2个.

- 将JSX的嵌套层级控制在3层以内。

    
### <h3 id='p5'>项目分支管理规范</h3>
#### 命名规范
* git 分支分为集成分支、功能分支和修复分支，分别命名为 master/dev、feature 和 hotfix
* 分支名称应包括类别, 开发者, 功能名称, 时间信息, 如 `feature/user/addSth0525`, `hotfix/user/fixHome0525`

#### 提交规范
* 提交备注建议描述详细.
#### 管理规范
* 功能开发提交测试前需合并最新master分支.
* 对于已经发布的分支, 需定期清理删除.

