## argparse python脚本入参
- [通用](###通用)
- [add_argument](###add_argument)
#### 通用
- parser.add_argument()，里面的参数，如果有–，表示是可选参数，没有–的话，意味着是必选参数，在运行时必须输入，default是没有用的。

### add_argument
```txt
name or flags：一个命名或者一个选项字符串的列表，例如：-f，–foo
action：当参数在命令行中出现时使用的动作基本类型
nargs：命令行参数应当消耗的数目
const：被一些 action 和 nargs 选择所需求的常数
default：当参数未在命令行中出现时使用的值
type：命令行参数应当被转换成的类型
choices：可用的参数的容器
required：此命令行选项是否可省略
help：一个选项作用的简单描述
metavar：在使用方法消息中使用的参数值示例
dest：被添加到 parse_args() 所返回对象上的属性名
```

