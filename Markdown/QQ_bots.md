# qq机器人开发学习笔记
## 我的openrouter.ai KEY(防止忘记)
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
## 我的智谱aiKET
e001c2dd74e640c1b82bbd3866846985.t8id09mn0yzaRt5V
## 一个来自deepseek的代码
```python
from nonebot.params import CommandArg
from nonebot.adapters import Message
from nonebot.matcher import Matcher
from nonebot import on_command

weather = on_command("天气")

@weather.handle()
async def first_handle(matcher: Matcher, args: Message = CommandArg()):
    """第一步处理：检查参数"""
    
    # 如果没有参数，等待用户输入
    if not args:
        await weather.pause("请输入要查询的城市名：")
    
    # 如果有参数，交给下一个处理器
    matcher.set_arg("city", args)  # 将参数存入状态

@weather.got("city")
async def second_handle(city: Message = Arg()):
    """第二步处理：获取城市名后的处理"""
    
    city_name = city.extract_plain_text().strip()
    # 处理天气查询...
```
## 写插件入门
- 包插件
插件文件夹内：
_init_.py #插件入口，必填，用接入NB2，注册功能+声明元信息
```
from nonebot.plugin import PluginMetadata

_plugin_meta = PluginMetadata(
    name = "", #插件名字 必填
    description = "", #功能描述 必填
    usage = "", #用法 必填
    version = "" #版本号 eg:"1.0.0" 选填
    author = "" #作者名，选填
    homepage = "" #插件主页，github 或 gitee链接
    supported_adapters = {""} #指定的适配器，例如QQ常用的{"~onebot.v11","~onebot.v12"}
    extra = {"":"","":""} #自定义额外信息，随便加，比如"tips":"免费查天气"
    type = "" #插件类型，自定义分类，eg:type = "工具"
    #config(配置类) ，eg:config= Config(需先from config import Config)
)

```
_config_.py
func.py(或者你想起的名字，比如weather.py) # 

## 插件下载禁用和卸载
nb plugin install 插件名下载
nb plugin uninstall 插件名卸载
nb plugin block 插件名
