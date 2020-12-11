```flowchart
st=>start: 许可协议选择
condOpen=>condition: 开放源代码

condcc=>condition: 禁止使用
copyright=>end: 私有 保留所有权利

condcreate=>condition: 禁止基于此进行创作
noncreate=>end: 禁止演绎

condshare=>condition: 禁止分享
nonshare=>end: 禁止分发

condcopy=>condition: 禁止分享更改
noncopy=>end: 禁止变更分发

condProfit=>condition: 禁止盈利
nonbusiness=>end: 禁止商业使用

condSpread=>condition: 衍生作品有时须开放源代码(传染)

condServise=>condition: 开放服务时要开源
agpl=>end: AGPL 3.0

condDll=>condition: 动态(运行时)连接要开源
gpl=>end: GPL 3.0

condLib=>condition: 静态(编译时)连接要开源
lgpl=>end: LGPL 3.0

condEdit=>condition: 直接使用经过修改后使用要开源
mpl=>end: MPL 2.0

condDescript=>condition: 需要附上修改的细节
apache=>end: Apache 2.0

condUsing=>condition: 不可利用贡献者的名义
bsd=>end: BSD
condName=>condition: 保留署名以及协议内容&著作权
mit=>end: MIT
public=>end: 公共软件

st->condOpen
condOpen(yes, right)->condSpread

condSpread(yes)->condServise

condServise(yes, right)->agpl
condServise(no, left)->condDll

condDll(yes, right)->gpl
condDll(no, left)->condLib

condLib(yes, right)->lgpl
condLib(no, left)->condEdit

condEdit(yes, right)->mpl

condSpread(no)->condDescript

condDescript(yes, right)->apache
condDescript(no, left)->condUsing

condUsing(yes, right)->bsd
condUsing(no, left)->condName

condName(yes, right)->mit
condName(no, left)->public

condOpen(no, left)->condcc

condcc(yes, right)->copyright
condcc(no, left)->condcreate

condcreate(yes, right)->noncreate
condcreate(no, left)->condshare

condshare(yes, right)->nonshare
condshare(no, left)->condcopy

condcopy(yes, right)->noncopy
condcopy(no, left)->condProfit

condProfit(yes, right)->nonbusiness
```
