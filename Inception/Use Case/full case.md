## 用户目标级别用例<br />
参照教程给出的full用例例子，编写了电影票售票系统的一个用户目标级别用例。<br />
----
- 范围：电影票售票系统
- 级别：用户目标
- 主要参与者：购票者
- 涉众及其关注点：<br />
	- 购票者：希望能够更加方便、便宜、快速地买到想要看的电影票，避免去电影院排队买票。希望能够方便的浏览最近的电影上映信息
	- 广告商：希望能够通过在售票系统上的广告投放，让更多潜在用户了解它们，达到比较好的宣传效果
	- 影院：希望通过在售票网站上卖票，提高电影票和小吃销量，赚取更多的利润
	- 支付授权服务：希望接收到格式和协议正确的数字授权请求。希望准确计算用户的应付款
- 前置条件：售票系统得到了影院授权，而电影的上映授权一般是影院自己获取的
- 成功保证：记录购票信息，影院生成相应售票记录并更新状态，用户获得购买凭证（二维码等）
- 主成功场景：<br />
	1. 用户登陆账号
	2. 用户挑选一部正在上映的电影
	3. 系统根据用户所处地理位置为用户推荐影院
	4. 用户挑选一家影院
	5. 系统筛选出这家影院关于这部电影的排片信息
	6. 用户挑选一个观影时间段
	7. 用户从剩余的座位中挑一个或若干个座位
	8. 用户选择一种支付方式支付
	9. 系统通过与支付授权平台的交互，完成从用户端扣费功能，并通知相应影院生成售票记录，更新售票记录
	10. 用户付款成功，并获得购票凭证，到时候就可以凭此凭证进入影院观影
- 扩展（或替代流程）:<br />
&emsp;A. 用户未登陆：当用户未登陆，就无法进入购票流程正常购票。<br />
&emsp;&emsp; 1. 进入购票流程（点击购票按钮）时，系统检测是否是登陆状态<br>
&emsp;&emsp; 2. 当检测到未登陆，跳转到登陆/注册界面<br>
&emsp;&emsp; 3. 登陆成功后返回系统首页<br>
<br>
&emsp;B. 多个用户同时购票冲突：当多个用户在同一时刻选择了相同时间的相同的座位并进行支付，则只能另其中更早的申请成功，否则会出现一个座位卖给多个用户的情况。<br />
&emsp;&emsp; 1. 用户点击支付按钮<br>
&emsp;&emsp; 2. 系统根据用户提交的订单信息查看座位是否真的空闲<br>
&emsp;&emsp; 3. 若刚刚已经有其他用户早一步定下位置，系统不生成订单，返回提示信息<br>
&emsp;&emsp; 4. 系统刷新页面，显示当前剩余位置<br>
&emsp;&emsp; 5. 用户重新选择座位<br>
<br>
&emsp;C. 用户支付失败或取消支付<br />
&emsp;&emsp; 1. 用户选择的支付账号余额不足，例如微信支付余额 < 票价<br>
&emsp;&emsp;&emsp;&emsp;&emsp; 1. 用户选择支付方式并支付<br>
&emsp;&emsp;&emsp;&emsp;&emsp; 2. 系统与支付服务平台交互，如果能够成功扣款支付成功，若无法成功扣款，返回提示信息（余额不足）<br>
&emsp;&emsp;&emsp;&emsp;&emsp; 3. 用户选择其他支付方式<br>
&emsp;&emsp; 2. 用户点击支付按钮后，系统生成订单，但用户迟迟不支付，或者主动取消订单 < 票价<br>
&emsp;&emsp;&emsp;&emsp;&emsp; a1. 系统生成订单，开始计时<br>
&emsp;&emsp;&emsp;&emsp;&emsp; a2. 用户主动取消订单<br>
&emsp;&emsp;&emsp;&emsp;&emsp; a3. 系统销毁订单<br>
<br>
&emsp;&emsp;&emsp;&emsp;&emsp; b1. 系统生成订单，开始计时<br>
&emsp;&emsp;&emsp;&emsp;&emsp; b2. 系统等待10分钟，用户还未完成支付，则销毁订单<br>
- 特殊需求：<br>
 需要精确的用户位置定位，以查找用户附近一定范围内的影院并将此影院列表提供给用户
