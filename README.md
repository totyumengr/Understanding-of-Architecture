# Understanding-of-Architecture
关于应用架构的一些理解和认知，欢迎交流探讨。本文关注在“道”层面，包括列举的一些例子也是为了逻辑支撑。而对于一些“术”层面的东西，笔者觉得直接参考[CNCF Landscape](https://landscape.cncf.io/)中列举的各种技术学起来就很好。

## WHY
曾经有一个面试官问笔者：架构，还不是一个学科，如果5年后你想出本书，你想写些什么？
这是个好问题（虽然最后没有去这家公司），值得深思。希望以下的一些观点、结论能够```部分回答```这个问题。

从宏观视角看，每代人都是```一个迭代```，和软件工程不同，这个迭代过程中继承下来的东西还比较少，几乎都需要重头开始。所以唯有文字是可以加速继承，拉齐认知的。笔者经常反思，假设自己可以早几年达到当下的认知水平，可能会发展更好一些。所以确实期望这些文字可以帮助到一些架构从业者，也借此描绘出他们的内心世界，给仍在这条路上继续前行的人一丝力量。

## 零、开篇
笔者从事软件行业已满15年了，回想整个行业的发展历程，真的是快到可怕，时至今日笔者觉得绝大部分从业者虽然在Coding，但某种意义上已经不是技术人员了。为什么这么说？笔者理解的技术人员是面对“不确定性”，解决“规模化”问题的一群人，按照这个标准，相信已经把很多人划出界外，因为在云计算快速普惠的时代，从纯技术层面已经接近解决。
那么是不是就这些技术人员是不是就没什么生存空间了呢？笔者的回答是：
- 如果不改变，是的，最终肯定会被Low-Code、RPA这些平台所取代，虽然他们现在看起来很“傻瓜”，很“笨重”。
- 要改变，要在技术平台的上一层中寻找问题域并抽象出这一层面的“存储、计算和网络”，组成Runtime，搭建平台。

**请一定记住，不要```对抗```技术！**

由于是在“道”层面的阐述，所以为了验证观点，笔者也例证了一些Case，有些Case并不是软件领域的，但万事万物的底层逻辑是相通的。架构师得具备一个“可视化”的能力，能够把数字世界的软件架构映射到现实世界中来。

#### 什么是技术和架构
1. 技术的价值是在低成本的机器上进行规模化 & 持续生产，而架构是通过对技术的组织，试图管理来自内外**不确定性** ，保证稳定的加速度，保持敏捷反应能力。从这个角度上来说，大家经常说的系统包袱重改不动，这里就是缺乏架构治理的表现了。仰望星空 & 脚踏实地，架构是Balance的艺术！
2. 技术支持产品，产品支持业务，技术需要解决业务场景中的```更高、更快、更强```问题。
3. 应用架构师 = 架构治理的框架，框架解决的是拉升基线问题，而不是全部。因此，作为应用架构师要确保的是参与应用的架构工作者们的“架构价值观”，“架构方向”，“架构方法”等因素是正确的。
4. 如上面的定义技术和架构是两个词。曾经碰到一个做基础架构的面试官，非常不屑笔者的应用架构领域，他认为这没啥技术含量，呵呵，这是非常狭隘的。因为都是解决不确定性的问题，那到底是基础设施层的不确定性问题多，还是业务应用层的不确定问题多？肯定是后者对吧。所以说千万不要以为技术是一切，现实的很多业务场景中技术是非常靠后的，事情能否做成其决定性作用的往往是商业模式、市场销售、产品运营。相对于狭义的技术来说架构的应用面就广了，大到一个大组织，小到一段代码，都需要有好的组织方式，而这就是架构。架构的好，就有非常强大的底座，相当于修炼了“九阳真经”，以后做什么业务都会非常快。

#### 怎么做架构
1. 和当初在学面向对象设计时一样，笔者的理解是多观察现实世界的一些事物，比如线程池的设计和平时咱们去银行办业务时被接待的场景是很像的；比如软件的模块架构，是不是和组织架构中常见的```N横M纵```类似。
2. 多和优秀的技术作品学习借鉴，把设计的理念套上去类比（不一定要非常严谨），沿着这个思路去想你要架构的事物，很多时候会有豁然开朗的感觉。比如笔者曾经深入研究过操作系统（OS）的设计，并把它移植到一个企业应用的架构设计里面，取得了很好的效果。
3. 架构无非就是拆与合，加入背后研发团队这个维度后，就升级到收和放的问题。怎么拿捏这个尺度呢？经常有人问有没有什么标准，我的回答都是没有（否则这就成了学科了是吧），但是可以告诉大家一个实操的经验：把你手上的事情排个序，挨个往外砍（把事儿交出去），砍到你不能接收了，剩下的就是收的部分。
4. 没有完美的架构，都是结合资源、成本、业务发展阶段、架构认知深度、行业技术发展等因素后的决策结果。比如为什么会出现传统数仓的架构：ODS/DMD/DMA/RDM，本质原因就是当时的技术处理不了那么多的数据，所以采用架构的手法解决；随着技术的进步，出现了实时数仓。笔者认为这才是行业上常说的“架构是演进出来的”观点的本质原因。

## 一、终局思维
1. 工程技术一直在追求两个方面：
   - **自动化**，Code化是基础，在云原生时代的整体技术Stack都是要求快速拉起的，才能够享受到云计算的便利（否则怎么能说是“本地人”，哈哈）。
   - **标准化**，保持API不动，切换Service Provider，也可以叫追求《NO Lock-in》。
2. 工程技术不断在Share-Nothing <-> Share-All之间演化，本质是一直在追求给应用分配一个自主可控的隔离环境，同时成本又很低。
3. 声明式和命令式其实是What和How的关系，最终想要的是What，所以声明式方法是应用系统的终极目标，这种API之上的境界。
4. 最终应用架构工作的落脚点只有两个：点和线（inspired from aPaaS&iPaaS by Gartner）。只不过要应用在架构的不同粒度，不同维度而已。

## 二、致架构工作者

做架构要求工作者要有全局思维，能够抓住关键点并提前布局，来赢得对**不确定性问题**的把控力。同时架构工作也避免不了会影响**利益的分配**，这并没有什么可忌讳的，各司其职才能协同共赢。

#### 坚守价值观
1. 通过概念抽象和代码框架解决业务应用研发过程中20%的问题就很好了，切忌不要想着100%。合理 & 可执行是追求，不能从一个极端到另一个极端。
2. 分离业务代码和非功能性代码是持续追求的，至于用框架来实现还是用基础设施层来实现这个是操作手法，会随着技术迭代进步而不同。
3. 站在未来看现在，这是很多架构工作者认同的认知方式，但未来是不可预测的，大家能做的就是“战略性”布局，用好资源提前下几步关键的棋。
4. 架构设计升级就应该对现有的技术组织、研发流程和配套工具等产生影响，这是变革式的，也是梦寐以求的机会。但更多时候是**微创新**，请记住无论影响大小，本质上都是一个词：改变。
5. 架构的目标用户是研发同学，架构师是一个**服务性工种**。要拒绝一切反人类的设计，因为在再牛的设计也需要其用户的认可。避免曲高和寡，若出现这种情况，大部分的真实情况是曲也不高。

#### 抑制自我膨胀的欲望
1. Cloud-Native Landscape的App Definition & Development只包括一部分业务块，这些是通用的，应用开发中还有一些通用的Server侧技术，比如工作流服务，但暂时未纳入进来，笔者觉得是经过思考权衡的结果。对架构工作者的借鉴意义就是：不要持续的做加法，记住永远无法囊括一切。越往上层，技术越会被细分，抽象程度过高反而非常难落地。
2. 继续【1】的思路，围绕【核心资源】展开架构工作，比如流量入口，偏底层技术支撑层，交付流水线，统一数据中心等等，要站在上帝视角看软件开发工作，用技术（解决规模性问题）方法解决。
3. 从Core Model（base on DDD）、Application Framework、Supporting Platform这三个角度来解构一个大型应用系统，是一个惯用的手法。不过请按顺序来，不要上来就搞最后一个。
4. 如何能把握的住架构实现？这个是架构师的终极困难。笔者的实践经验是：靠人+组织的力量，具体就是找到合适的人守住关键的技术资产。因为你无法完全掌控全局，没有Power，也没那个精力能具体到每一个点。
5. 架构工作者需要了解业务，但这更多指的是了解业务的“未来”，而不单单是“现在”。笔者的经历中遇到过很多Case，以为跟着某一块事情一路走过来，对细节很清楚，就肯定是个好的架构师，结果长线看还真不是，甚至是不合格的。究其原因，这里面有很多Case是因为无法做到“不破不立”。

#### 行为建议
1. **别做“闷葫芦”**，不要轻易憋大招。要经常与技术骨干们沟通，多听他们的“吐槽”。笔者本身不是一个外向的人，但职责所在也没办法。经常性的帮别人分析问题，答疑解惑，是给自己“信用”充值的好方法。可以说支撑架构师的核心要素之一就是信任。
2. **不要“说教”**，允许工程师做创新，而创新就意味着失败，架构师要做的事，管理失败的影响范围。切忌不可“大包大揽”，不要试图成为某个技术团队的天花板。类比算法Model的训练过程，是需要不断试验调参的，而架构师的认知Model也是需要这个过程的，这样的准召率才会高。
3. **注重“技术外交”**，一方面和公司内的技术组织保持同步，打造团队技术品牌；另一方面多和行业接轨（包括参加技术大会，发表技术文章），提升技术骨干的个人影响力，打造技术明星。对一个技术团队来说这个工作非常重要，因为对工程师来说能有提高自己技术实力的机会，有时候胜过收入高一些的诱惑，当然都有就完美了。
4. **保持“独立思考”**，不要长时间把所有精力都放进某个具体技术的开发中，做好“裁缝”的角色。平时能够敏锐的找到薄弱点修修补补，关键时刻敢于断臂求生开着飞机换引擎，能做到这样的前提就是“站在上帝视角看问题思考对策”。
5. **敢于“Say No”**，关键时刻要承担起架构师的责任。很多时候是要往回拉一拉研发同学，帮助技术负责人把控风险。好技术有很多，关键是能用好。
6. **谨慎的发明名词**，技术名词的多少很大程度上代表了技术领域的火热度。工作中碰到过很多同学喜欢发明技术名词，本身没错，要做一个事情得师出有名。但关键问题是大多数同学无法解释这个名词的含义，无法清晰的说出和现有技术名词的差异点。这就得怀疑他自身的架构素质了，是否有想清楚，还是只是炫技。

## 三、做架构要知道的事
#### 客观规律
1. 谨慎使用trick的方法，一板一眼是最好的，架构的目标系统越大越是应该如此，可以想象为是在开一个大船，肯定不能像开快艇一样。同时也要避免“照本宣科”，应该要有一定的Localization。
2. “统一处理”这个是相对普世的一种价值观，逻辑分散是常见的架构治理问题。同时要把握好度，最怕的情况是逻辑“飞了”，并不是强制要归一，很多时候归二、归三也是OK的。这里面是有康威定律在起作用的。
3. 库→框架→脚手架→中间件→开放平台→低代码开发平台，这条架构赋能链路是大部分架构工作者的工作目标路径。底层的驱动力就是关注点分离。
4. 系统化→数据化→智能化，这是架构工作发力的三大维度。不同的系统根据其所处的生命周期阶段，架构师要关注不同的维度的价值提升，会有事半功倍的效果。就像人类一样，要先有生命（有身体、脉络，大脑，然后再有血液传输）再有灵魂（进行思考、产生思想）。
5. 保持对系统的***可控性***，这是功力的体现。前提是可观察性，也就是上面说的【数据化】阶段。
6. ***自由***是有代价的。对于软件系统来说也是这样，越灵活越难，需要深厚的技术底座来支撑。

#### 提升基线，技术普惠
1. 哪有什么岁月静好，只是有人替你负重前行。这句话同样适合于技术届，一小撮技术牛人就在做着这些技术普惠的事情。
2. 业务开发就像是甲方，其他都是【技术供应商】，而供应商不能绑架业务，只能助力业务，从而完成技术普惠的使命。
3. 基础云业务商可以类比房地产开发商，他们用规模化的标准产品推动基础设施现代化，标准化之后，自然催生了更多业务垂直、行业垂直的供应商来服务“客户”。这个笔者认为是他们最大的价值，也是整个生态繁荣的催化剂。
4. 要向产品同学对待客户一样，仔细推敲目标用户的类型，根据场景不同提供不同的能力，就拿API来说，有High Level和Low Level，应该把Low Level交付给专业开发者，而把High Level的交付给用户。
5. 要区分出不同的技术场景，分别使用SPI or API的暴露方式。拿建筑行业类比一下：```SPI是开放给建筑工人的，而API是开给装修工人的```，很显然对开发者的要求是不一样的。用SPI来提升基线能力，用API来做技术普惠。

#### 周期性规律
1. 技术总是在进步的，只不过细分技术处在周期中的哪个阶段。之前后端热，然后移动端热，当下（2020）算法热，之后会是什么，笔者判断是应用架构。更重要的是自己平时的积累与沉淀，属于自己的周期总会来的。
2. Framework/Runtime和CI/CD，这一里一外是个双循环上升的关系。当规模小的时候是前者是重点，当规模大的时候就轮转到后者了。笔者觉得这个是例外是动态的关系，比如在Web架构与Serverless架构模式中，这些事物都存在，只不过是里and外的两个极端。
3. Gartner有个著名的技术炒作曲线，刻画着每个技术的不同生命周期阶段。当然在真正严肃的线上环境中，对待新技术的建议是“谨慎的乐观”。笔者在百度工作的前期，经常听到一句话：引进新技术可以，但要能Cover住。说白了，每个技术都有优势有坑，就看你知不知道坑在哪里。

#### 无权管理
1. 在研发团队中，很多时候对架构师的工作并没有清晰的定位，有当高级工程师用的，有当吉祥物对外宣传用的，有当管理者技术助理用的，等等，总之是一个“无权”的状态。那么如何能发挥作用，心想事成？最基础有两点：一是能救火，二是能布道。这是能帮你打开局面的关键要素。
2. 审时度势，也就是```WHEN```，这个是最难的部分。要知道很多时候架构师说的都是有道理的（毕竟拿那么多钱是吧，哈哈），同样很多时候把握不好时机，也办不成事儿，久而久之心灰意冷。请记住当前的大环境是这样的。说早了争取不到资源，说晚了又体现不出价值。
3. 和技术主管申请设立技术管理组织（比如架构组）将技术骨干组队，这样由这个组织经过充分讨论做出来的决策会更加有Power。一切从纯技术角度出发，虽然无权，但是会有权威。还有另一个好处，从“自说”变成“他说”，架构决策经由每个技术骨干认可后的传达会更有效率，有时候比起你亲自对接研发团队的效果更好。
4. 向组织要两个关键“抓手”：技术晋升标准、技术资源管理，别小看这两个权力，这两个事情能否覆盖到研发同学的方方面面。就好比CEO一定要把控好人事权、财权一样，具体业务怎么干可以交给COO，而做事情的核心命脉，人和钱两项是必须把控的。

## 四、一些常见的架构误区
1. 分层架构是大家最常见的架构手法，而这里面最常见的错误是上层与下层的能力都差不多，没有明显的区别。例如写Web后端最常用的Controller-Service-Dao-Mapper，Controller和Service之间的定位差别非常清楚，但大部分的代码中Service、DAO、Mapper定位不清楚，层与层之间的能力差别不大，都是转发。所以这就是笔者说的照本宣科。用在代码里还凑合，如果用在大型系统中，只是徒增复杂度。
2. 工程师是一个充满创造力的工种，经常要“发明”一些东西，比如写一个框架、设计一个DSL，这是好事儿需要鼓励。但笔者经历过很多乱用的现象，往往是作者很Happy，其他人很懵逼。很多时候为了解决一个问题，创造了一个东西，但很不幸这个东西如果过于复杂，它就变成了一个更大的问题。举个例子，之前碰到过一个设计权限系统的Case，大家知道功能权限相对容易，数据权限的控制表达很难，当时这个作者为了达到数据权限控制的可配置化，搞了一套表达式，在管理平台上开放给产品运营使用。但估计大家猜到了，随着场景的增多，表达式越来越复杂，最后产品运营同学根本配不出来，只能作者自己上（他也不敢保证能写对）。这个Case怎么解的呢？笔者给出建议把提供Service，改成提供Framework，分散出去让各垂直场景自行解决抽象。
3. 一个偏业务端应用的团队随着迭代的进行，会对外团队提供一些API、数据交换的事情。从组织架构、系统架构上看来都是不对的，这会导致网状模型，是一个架构的大忌。解决的办法就是下沉，最好的情况是单独拉出共享服务团队来提供服务，如果组织上拆不开，托底也应该技术层面的独立服务。
4. 在做业务建模时，有时候会自然的以业务流程为主线进行，这样做出来的系统自然不会错，但如果评价这个模型好不好，设计功力行不行的时候，很多情况下不一定那么好。举个例子：要设计一个账户系统，很自然要设计超级管理员，管理员，普通用户，并设计权限控制系统，之后的一切围绕账号展开。
如果这个账户系统放到ToC业务或者简单的ToB业务中，笔者相信OK。但如果是复杂的ToB业务中，就会比较困难，比如ToB业务的服务对象是企业，而企业的组织架构怎么表达，组织架构内不同部门间的数据权限如何管控，业绩如何迁移等等。所以在笔者看来**所谓建模就是如何优雅的表述和处理对象间的关系**，且这里面重要的一点就是```先抛离系统```，从事实出发进行业务抽象。组织是一直存在的客观对象，客户是它在某个系统内的概念，而组织并不一定会使用这个系统。

## 附录一、对于大热的DDD的评价
1. DDD是一个复杂业务的落地项目合作框架，指导和约定从业务到技术的基本关键点。
2. DDD在代码层面的指导意义不大，在业务组件（微服务）粒度应用的性价比最高。
3. 从复杂多变的业务中分离出稳定的业务or技术层，这才是本质，DDD在这方面只是个方法。

## 附录二、到底什么是Low-Code
1. 从目标用户角度它解决的是非专业开发者的应用构建门槛问题。实际环境中笔者发现了一些Case，明明是针对专业开发者做的一些工具，还叫“Low-Code”。
2. 从产品功能角度它达到的效果应该类似Excel之于数据处理般的效果，使它的用户能够非常简单便捷的设计出专业的企业应用类软件。
3. 从技术架构角度实现它必须是Metadata-Driven的，绝对不能是Form-Driven，笔者和前端工程师合作时他们比较难理解这两者的差异，Low-Code不等于妥妥拽拽的可视化开发。

## 附录三、架构师要不要写代码
1. 如果架构师懂代码，写过代码，将非常有助于你的架构生涯。因为万事万物的规律是想通的。
2. 不要追求代码量，当下的技术环境是非常开放的，新一代工程师们的代码能力会越来越强，可完全委以重任。
3. 建议不要扔下这个技能，至少还能辅导你的小朋友呢，技多不压身嘛。

## 附录四、架构图是什么
1. 要做到**一图胜千言**，架构图是架构的可视化结果，如果看不明白，更多的时候不是太复杂，而是表达问题。
2. 由外到内，步步拆解描述这个“架构物”，第一步先用外部视角看，把它当一个黑盒，描述清楚它和外部世界的关系；第二步先纵向自顶向下切一刀，描述清楚内部模块的逻辑关系，重点是和外部的通讯接口部分；第三步挑出少量核心模块进行描述，包括核心业务流程，核心数据模型，核心技术难点等。
3. 不要全部都画那种块块堆砌的架构图，这种图更多时候用来表达业务架构、产品架构，技术的架构图中要有线来串联。当然技术也是有“产品”的，比如云上就有很多技术产品。

## 附录五、什么是多租户
1. 所谓多租户，租的是**核心资源**的使用权，需要确保在租期内可被私有合规使用。当然操作核心资源需要工具，工具可以免费，也可以付费，这个基本逻辑关系一定要弄清楚。
2. 支持多租户的系统一定围绕其核心资源搭建一个管理模块形成Kernel，向外暴露API接口和开发工具包，再联合一些支撑型组件形成”OS or Infrastructure“。拿广告业务举例，这个核心资源就是流量资源，广告主都是在抢夺能曝光的机会而已。管理模块就是Ad-Server(广义的，包括算法)，由它来确保对流量资源的安全&高效实用。”OS“层就包括了账户、财务、物料、人群、数据等组成的系统级服务，这三层事物加起来，就形成了一个多租户基础设施。
3. 在SaaS系统中的多租户基础设施，通常需要解决以下几个问题：
   - 数据隔离：分为租户粒度、应用间粒度、应用内粒度
   - 定制隔离：UI/Logic/Data/Process的定制，并且不影响其他租户
   - 系统可用：系统升级对平台本身和运行中的定制应用无影响   
4. 多租户基础设施 + 开发平台 = Application PaaS，这个是企业级应用未来的基础生产力平台。

## 附录六、一般的服务拆分原则都有什么
1. 迭代变化节奏差别非常大的，比如偏技术的模块和偏业务的模块就需要拆分开
2. 业务所属的组织不在一个总监（确实找不到合适的代表名词，一般总监都各自有一摊业务范围，并且需要关注技术架构，所以就先用这个）下的，比如偏前台的和偏中台的组织提供的服务需要拆分开
3. 考察的核心技术指标不一样的，比如ToC系统考察高并发高可用，ToB系统考察可配置可扩展，这两者也需要拆分开
4. 技术领域完全不同的，比如偏前端的模块，偏算法的模块，偏大数据技术的模块，需要拆开
5. 服务用户/客户类型不一致的，比如运营端、商家端、用户端、开放平台端等，常规条件下需要分拆

## 附录七、故事线为什么那么重要
1. 逻辑思维能力是理科生的专长，为什么大多数是理科生的程序员一般表达上不清楚呢？对架构师来说是非常致命的，那么解决的办法就是：构建故事线。
2. **WHY->WHAT-HOW**，按照这个方式来递归解释一个复杂事物，会比较容易的让人理解，也比较能和人找到共识。
3. 一个好的故事需要有观点、有案例、有思考、有总结，架构工作者应该有讲“故事”的能力。

## 附录八、为什么说认知能力那么重要
1. 认知是建立在全面的信息了解之上的，这就要求视野足够开阔，先把能吸收的都吸收进来，消化不了再扔掉。
2. 位置越高的人，认知能力越重要。认知是能指导行动的，它是能做成事情的灵魂，远比事无巨细的规定、流程、标准管用。因为定的越细，漏洞越大。
3. 架构师需要深入的分析某个事物，做一个决策背后需要考虑的因素很多，很多时候是矛盾的，脑袋里面有两个对立的观点。大家会说遵照使命愿景价值观来决策，没问题这是对的，但怎么把当下这个决策和他们正向的联系起来，还是需要认知能力。

## 附录九、工程效率是架构师的关注面么
1. 在云原生的时代，工程效率越来越体现出它的重要性，以为它是微服务架构风格能够取得实效的重要保证手段。
2. 工程效率提升，核心思想是数据驱动，指标可视化。它追求的是标准化的生产制造模式，在云原生进化到```以应用为中心```的阶段，是非常需要弥合它与```以资源为中心```的基础设施的。
3. 工程效率的问题，当前已经到了用技术来解决的阶段，其核心原因是因为云计算带来的规模化效应，使得必须重构原来的“作坊式”运作模式，转而是更加标准的工厂流水线模式。
