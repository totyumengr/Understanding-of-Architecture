# Understanding-of-Architecture
关于应用架构的一些理解和认知（随笔，未经结构化整理），欢迎交流探讨。

## 技术架构工作的价值体现
1. 技术的价值是在低成本的机器上进行规模化 & 持续生产，而架构是通过对技术的组织，试图管理来自内外[不确定性] ，保证稳定的加速度，保持敏捷反应能力。
2. 工程技术一直在追求《自动化》，因为这个是支撑【1】的基础、必要条件之一；另一个方向是《标准化》，保持API不动，切换Service Provider，也可以叫追求《NO Lock-in》。
3. 工程技术不断在Share-Nothing <-> Share-All之间演化，本质是一直在追求给应用分配一个自主可控的隔离环境，同时成本又很低。

## 对于大热的DDD，我的评价
1. DDD是一个复杂业务的落地项目合作框架，指导和约定从业务到技术的基本关键点。
2. DDD在代码层面的指导意义不大，在业务组件（微服务）粒度应用的性价比最高。
3. 从复杂多变的业务中分离出稳定的业务or技术层，这才是本质，DDD在这方面只是个方法。

## 架构工作者的价值观
1. 通过概念抽象和代码框架解决业务应用研发过程中20%的问题就很好了，切忌不要想着100%。合理 & 可执行是追求，不能从一个极端到另一个极端。
2. 分离业务代码和非功能性代码是持续追求的，至于用框架来实现还是用基础设施层来实现这个是操作手法，会随着技术迭代进步而不同。

## 提升基线，技术普惠
1. 哪有什么岁月静好，只是有人替你负重前行。这句话同样适合于技术届，一小撮技术牛人就在做着这些技术普惠的事情。
2. 业务开发就像是甲方，其他都是【技术供应商】，而供应商不能绑架业务，只能助力业务，从而完成技术普惠的使命。
3. 基础云业务商可以类比房地产开发商，他们用规模化的标准产品推动基础设施现代化，标准化之后，自然催生了更多业务垂直、行业垂直的供应商来服务“客户”。这个我认为是他们最大的价值，也是整个生态繁荣的催化剂。

## 抑制自我膨胀的欲望
1. Cloud-Native Landscape的App Definition & Development只包括一部分业务块，这些是通用的，应用开发中还有一些通用的Server侧技术，比如工作流服务，但暂时未纳入进来，我觉得是经过思考权衡的结果。对架构工作者的借鉴意义就是：不要持续的做加法，记住永远无法囊括一切。越往上层，技术越会被细分，抽象程度过高反而非常难落地。
2. 继续【1】的思路，围绕【核心资源】展开架构工作，比如流量入口，偏底层技术支撑层，交付流水线，统一数据中心等等，要站在上帝视角看软件开发工作，用技术（解决规模性问题）方法解决。
3. 从Core Model（base on DDD）、Application Framework、Supporting Platform这三个角度来解构一个大型应用系统，是一个惯用的手法。不过请按顺序来，不要上来就搞最后一个。

## 周期性规律
1. 技术总是在进步的，只不过细分技术处在周期中的哪个阶段。之前后端热，然后移动端热，当下（2020）算法热，之后会是什么，我判断是应用架构。更重要的是自己平时的积累与沉淀，属于自己的周期总会来的。

## 终局思维
1. 技术支持产品，产品支持业务，技术需要解决业务终局场景中的“更高、更快、更强”问题。
2. 声明式和命令式其实是What和How的关系，最终想要的是What，所以声明式方法是我们应用系统的终极目标，这种API之上的境界。
3. 最终应用架构工作的落脚点只有两个：点和线（inspired by Gartner的aPaaS、iPaaS）。只不过要应用在架构的不同粒度，不同维度而已。

## 做架构的若干基本原则
1. 谨慎使用trick的方法，一板一眼是最好的，架构的目标系统越大越是应该如此。同时也要避免“照本宣科”，应该要有一定的Localization。
2. “统一处理”这个是相对普世的一种价值观，逻辑分散是常见的架构治理问题。同时要把握好度，最怕的情况是逻辑“飞了”，并不是强制要归一，很多时候归二、归三也是OK的。这里面是有康威定律在起作用的。
3. 库→框架→脚手架→中间件→开放平台→低代码开发平台，这条架构赋能链路是大部分架构工作者的工作目标路径。底层的驱动力就是关注点分离。
4. 系统化→数据化→智能化，这是架构工作发力的三大维度。不同的系统根据其所处的生命周期阶段，架构师要关注不同的维度的价值提升，会有事半功倍的效果。
