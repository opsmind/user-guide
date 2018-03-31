使用自定义的脚本插件功能，您可以将任意自定义指标数据打入 OpsMind 系统中，非常简单。

使用方法如下：

1. 编写标准输出格式符合规范的可执行程序（例如脚本）
2. 将脚本放入任意安装了 OpsMind Agent 的服务器的 `/var/lib/om_plugin/` 目录下

OpsMind Agent 将以 30 秒的间隔自动运行（不带参数运行）该目录下的所有脚本，并将脚本的输出收集上去。

#### 脚本的输出格式

脚本的输出格式需符合以下格式：

```
<metric_name>{<label_name>="<label_value>", ...} <metric_value>
<metric_name>{<label_name>="<label_value>", ...} <metric_value>
...
```

其中：

1. `<metric_name>` 为该指标项的名称，只能 **由字母与下划线组成**
2. `<label_name>` 为标签名称字符串，只能 **由字母与下划线组成**
3. `<label_value>` 为标签值字符串
4. `<metric_value>` 为浮点数数值
5. `{` 和 `}` 内可以没有任何标签

一个合法的输出如下所示：

```
process{} 800
cpu_usage{cpu="cpu0", mode="idle"} 12345
cpu_usage{cpu="cpu1", mode="idle"} 12345
mem_usage{mode="free"} 400000
mem_usage{mode="used"} 400000
```

注意点：

1. 相同指标名称的标签种类需保持一致
2. 脚本的输出标签中无需包含执行脚本的服务器标识，因为 OpsMind Agent 会自行添加此标签（`host` 标签）


#### 脚本指标项的查看

一个新的自定义指标项一旦被收集，在一分钟内就可以自动在控制台的 `监控指标` 菜单里被列出。数据查询方法与其他指标项相同。

