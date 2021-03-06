# CoR (责任链模式)

###诞生背景（能解决什么问题）

- 例如：博客系统，可能需要判断（1）用户是否登录，（2）用户是否有页面访问权限（3）用户是否有增删改查权限（4）…… 
- 以上谈到的就是一条权限验证链，如果没登陆，那么可能后续的验证就不需要检查了，直接返回验证失败等信息即可。
- 还可能过了几个月，程序受到网络攻击，或者需要增加黑名单等等，如果只是堆砌代码，只会臃肿不堪，最终不得不重构代码。
- 当然不仅仅是验证时使用这个模式。很多其他情况也可以（只要是符合这种链式的）

###概述
- 在上述示例中， 每个检查步骤都可被抽取为仅有单个方法的类（我们把这个类叫做处理者类）， 并执行检查操作。
- 模式建议你将这些处理者连成一条链。 链上的每个处理者都有一个成员变量来保存对于下一处理者的引用。(就好比是链表)新增，修改，删除都更便捷。保存下一处理者的成员变量就像是指针。
- 责任链模式也可以理解为`if...elseif...elseif...else`，判断条件可以根据需求适当调整（增删或改顺序）
- 每个处理者类都必须实现相同的接口（便于维护和扩展）

###实际案例

- http请求中间件
