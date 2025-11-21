
# 李跳跳app+规则合并去重工具+布局查看工具

可以跳过开屏广告的安卓手机软件工具。其范围广、精确高、有效“干掉”广告的特点受到众多网友好评，被戏称为“互联网药神”。

# [autojs-4.1](https://github.com/enjoyDay/my-autojs4)；附-脚本打包插件（js-to-apk-4.1.0 Alpha2-release）；附：LiTool-李跳跳自定义规则编写辅助工具，配合autos可免修改粘贴。
[界面分析](https://github.com/SongYeXiaoLuo/Xiaoluo.spy/releases)；[李跳跳规则示范及说明](https://github.com/lhj1618GitHub/litiaotiao-leitiaotiao-android-app/releases/download/20251014/litiaotiao_sample.txt)


# [李跳跳网站](https://litiaotiao.cn/)；[GitHub-李跳跳](https://github.com/rongzhiy/LiTiaotiao)；[李跳跳进阶指南](https://litiaotiao.cn/posts/litiaotiao_advanced_guide/)

# [Touch-Helper](https://github.com/zfdang/Android-Touch-Helper/releases)：开屏跳过，仅使用无障碍服务；可采集控件信息/添加坐标点击/修改目标文字；资源占用最低；

# [GKD](https://github.com/gkd-kit/gkd)：功能更强；订阅式规则，自定义难度更高；使用管理员权限，可选shizuku；

# 更多功能

跳过广告提示语；微信自动登录；微信自动查看原图；微信自动勾选原图；QQ自动登录；QQ自动查看原图；网易云更新弹窗；抖音更新弹窗；其它任意弹窗


# 启用李跳跳

打开软件，点击开启->无障碍->更多已下载服务->李跳跳->打开开关。

<img width="970" height="560" alt="image" src="https://github.com/user-attachments/assets/0f01c4bb-8077-459a-89d5-50127fffa968" />


# 

[利用autojs获取控件信息](https://litiaotiao.cn/posts/use_autojs_to_get_control_information/)

[李跳跳实用规则示例](https://litiaotiao.cn/posts/litiaotiao_share_practical_rules/)


[自定义规则](https://github.com/Snoopy1866/LiTiaotiao-Custom-Rules/tree/main)

[下载规则合集json文件](https://litiaotiao.cn/AllRules.json)



# [李跳跳进阶指南](https://litiaotiao.cn/posts/litiaotiao_advanced_guide/)

注意：小白萌新不需要看这份进阶指南，使用默认设置已经可以跳过绝大部分广告了。

李跳跳的原理：利用安卓系统的无障碍权限，帮助用户自动点击广告上的跳过按钮。

##  李跳跳自定义规则

### 开屏广告规则

{"keywords":["xxx"]}、{"keywords_append":["xxx"]}

李跳跳默认规则已经可以跳过绝大部分开屏广告了，但李跳跳也不是万能的。

当我们遇到无法跳过的开屏广告时，可以使用这条规则：{“keywords”:[“xxx”]}。其中xxx可以是跳过按钮的文案，比如{“keywords”:[“关闭广告”]}；也可以是跳过按钮的id或bounds，比如：{“keywords”:[“tv_close_button”]}、{“keywords”:[“900,160,1170,250”]}。

【知识点】：什么是控件的id和bounds

### 参数 keywords 和 keywords_append 的区别：

keywords 会覆盖默认规则。

keywords_append 在默认规则的基础上，追加规则。

### 弹窗规则

{"popup_rules":[{"id":"xxx","action":"xxx"}]}

我们也可以使用李跳跳来关闭应用内的弹窗 ，比如下图所示的抖音更新弹窗，就可以用{“popup_rules”:[{“id”:“检测到更新”,“action”:“以后再”}]}规则进行关闭。这条规则的意思是：当检测到「检测到更新」这几个文字的时候，就自动点击「以后再」这个按钮。

抖音弹窗

细心的你会怀疑上面的规则是不是写错了，为什么参数action的值不是以后再说而是以后再？其实我是故意为之，目的是为了引出以下知识点：规则里面的文字默认情况下是模糊匹配的。比如改成以后、以后再说、再说，甚至后再都是可行的。

规则里面的文字默认是模糊匹配的，自然也支持首尾匹配和全匹配，只需在文字前面加上特定的符号就行。参照下面的举例张三，比如+检测到的意思是匹配以检测到开头的文字；比如-用户体验的意思是匹配以用户体验结尾的文字；比如=以后再说的意思是匹配和以后再说完全相等的文字。其中符号&是用来连接任意个条件的，你可以把它理解为且。

举例张三：{“popup_rules”:[{“id”:"+检测到&-用户体验",“action”:"=以后再说"}]}

有时候我们会遇到一些弹窗，它们的关闭按钮不是文字，而是一个叉号❎ ，比如下图所示的美团弹窗，此时我们又该如何写规则呢？

### 美团弹窗

分两种情况：

如果这个弹窗可以通过手机的返回键关闭，我们可以这样写规则{“popup_rules”:[{“id”:"=天天神券",“action”:“GLOBAL_ACTION_BACK”}]}。其中的GLOBAL_ACTION_BACK是固定不变的。

如果这个弹窗不可以通过手机的返回键关闭，我们需要知道叉号的id或bounds才行。假设这个弹窗的叉号的id是tv_close_button，我们可以这样写规则{“popup_rules”:[{“id”:"=天天神券",“action”:“tv_close_button”}]}。

但很多时候叉号(弹窗的关闭按钮) 不一定会有id，不过也没关系，因为它一定会有bounds。假设叉号的bounds是500,900,620,1020，我们可以这样写规则{“popup_rules”:[{“id”:"=天天神券",“action”:“500,900,620,1020”}]}。

【知识点：什么是控件的id和bounds?】

### 设置强制点击

{"click_way_popup":1}

详情参考：我的规则正确，但无法关闭对应弹窗怎么办?

### 设置搜索次数

{"search_times_popup":5}

详情参考：我的规则正确，但无法关闭对应弹窗怎么办?

### 设置延迟点击

{"delay":200}

开屏广告延迟点击：{“delay”:200}

弹窗延迟点击：{“delay_popup”:200}

温馨提示：单位毫秒，1秒等于1000毫秒。

### 设置点击次数

{"popup_rules":[{"id":"xxx","action":"xxx",times:2}]}

有些规则是不用点击的，此时我们可以把点击次数times设置为0；有时候我们会遇到两个不一样的弹窗，但它们可以用同一条规则来关闭，此时你可以选择输入两条一模一样的规则，或者输入一条规则但把它的点击次数times设为2；

### 联合规则

{"unite_popup_rules":true}

我们上面举的例子，关闭抖音更新弹窗和关闭美团天天神券弹窗，这两个任务都是瞬间任务，用一条规则表示就行。

但有些任务是持续任务，它们的耗时是不确定的，至少需要两条规则表示才行。比如有一个按钮需要倒计时100秒后才能点击，此时我们可以这样写规则：

把这个过程的中间态用一条规则表示：{“id”:“还剩&秒”,“action”:“还剩&秒”,times:0}

把我们需要点击的按钮用一条规则表示：{“id”:“弹窗”,“action”:“关闭按钮”}

设置参数unite_popup_rules的值为true。

所以如果想点击一个100秒后才能点击的按钮，完整规则应该是：{“popup_rules”:[{“id”:“还剩&秒”,“action”:“还剩&秒”,times:0},{“id”:“弹窗”,“action”:“关闭按钮”}],“unite_popup_rules”:true}

【温馨提示】：利用联合规则我们可以完成很多🌱耗时不确定的任务🌱，比如应用自动安装、微信自动查看多张原图等。


根据CheckBox的状态点击控件

CheckBox控件有两种状态，一种是选中状态，另一种是未选中状态。假设某个CheckBox控件的bounds是100,200,300,400，如果我们要点击它的其中一种状态，可以在bounds的后面追加数字0或1来表示，比如：

已选中状态：100,200,300,400,1

未选中状态：100,200,300,400,0


### 什么是控件的id和bounds

我们把APP界面上的元素，比如按钮、图标、输入框这些统称为控件。比如取消按钮它就是一个文本控件，它的文字就是取消。我们写规则时可以根据取消这两个字来定位这个按钮。但有些按钮它是没有文字的，比如上面美团弹窗的叉号按钮。此时我们需要用到控件的id或bounds来定位这些没有文字的按钮。

但什么是控件的id和bounds呢？控件的id就是控件的身份证(普通用户可以简单这样理解)；控件的bounds就是控件的大小和位置信息。

温馨提示：一个控件是有可能没有id的，但一定会有bounds。

如何获取控件的id或bounds

我们可以通过特定的工具开源APPautojs来获取到控件的相关信息,利用autojs 获取控件信息。

# 常见问题

### 我的规则正确但无法关闭对应弹窗怎么办

首先，判断你的任务是瞬间任务还是持续任务？如果是瞬间任务， 在确保你的规则是正确的前提下，可以试试以下两个方案：

如果有跳过提示，设置强制点击就行：{“popup_rules”:[], “click_way_popup”:1}

如果没跳过提示，延长搜索次数就行：{“popup_rules”:[], “search_times_popup”:5}

温馨提示：搜索次数 search_times_popup 越小越省电，最好是个位数。

如果是持续任务， 可以参考上面的联合规则章节。

### 出现误点怎么办？

首先，先删除自己的自定义规则，看看是否是自己的规则造成误点。

其次，在少数情况下，李跳跳的默认规则也会出现误点 (错误地点击了其它地方)，最简单的解决方案就是在李跳跳里面找到目标APP，把它加入白名单。

其次，你也可以用参数keywords来覆盖默认的规则，也就是说你自己告诉李跳跳应该点击哪里，比如：{“keywords”:[“500,900,620,1020”]}。

### 不知道某个弹窗属于哪个APP怎么办？

通过autojs软件获取这个弹窗任意控件的控件信息，复制控件信息里面的包名 (packageName) 信息，通过包名在李跳跳里面搜索对应APP就行。


# END

