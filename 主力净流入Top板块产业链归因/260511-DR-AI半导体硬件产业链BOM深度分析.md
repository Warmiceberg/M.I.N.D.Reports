**

# AI与硬件产业链物理穿透及底层逻辑深度审计报告

在人工智能从算法模型演进为全球规模化基础设施的进程中，算力产业正在经历一场与物理学极限的正面碰撞。当大语言模型（LLM）的参数量向万亿级别跃升时，支撑其运行的硬件基础设施已全面突破了传统摩尔定律的框架。当前的产业瓶颈不再仅仅局限于逻辑芯片的架构迭代，而是下探至光刻机的光罩物理极限、电磁波的信号衰减红线、分子层面的高频基材热力学特性，以及电网基建的极限承载力。本审计报告基于产业链物理穿透与底层逻辑解构框架，针对核心算力大脑、互联与通信神经网、底层物理载体及BOM（物料清单）解构，以及热力学极限与算电基建等四大核心赛道，执行深度穿透与审计。

## 算力大脑与链主生态审计

在当前的人工智能资本开支超级周期中，算力核心层的价值分配呈现出极端的寡头垄断特征。以英伟达（NVIDIA）、谷歌（Google）以及台积电（TSMC）为代表的“链主”，不仅掌控了技术标准的话语权，更通过其绝对的产能与生态壁垒，主导了整条全球供应链的价值吞噬。

### 链主霸权与物理极限下的架构突变

半导体制造的物理限制已经从根本上改变了AI芯片的设计范式。以英伟达的架构演进为例，Hopper架构（H100）代表了单片硅晶圆（Monolithic Die）的物理极限 1。H100在台积电定制的4N工艺下，将800亿个晶体管硬塞入814平方毫米的芯片面积中 1。这一面积已经触及了极紫外光刻机（EUV）单次曝光光罩（Reticle）的物理上限，即约800平方毫米的掩模版极限 1。

为了突破这一物理限制并继续呈指数级推升Tensor Core（张量核心）的算力密度，英伟达在Blackwell（B200）架构上被迫实施了“架构变异”，即采用双裸片（Dual Die）设计 1。B200将两块独立的GPU Die通过高达10 TB/s的NV-HBI（英伟达高带宽接口）进行物理连接，其传输速率之高、延迟之低，使得软件层完全将其视为一颗单一的GPU 1。这一物理架构的妥协与创新，使得B200在台积电4NP工艺下，能够在约1,600平方毫米的面积内容纳2080亿个晶体管，实现了相较于H100高达2.6倍的晶体管数量飞跃 1。

|   |   |   |   |
|---|---|---|---|
|架构规格对比|Hopper H100|Blackwell B200|代际提升倍数|
|晶体管总数|800亿|2080亿|2.6x|
|物理裸片配置|单裸片 (814 mm²)|双裸片 (~1,600 mm²)|~2.0x 面积|
|HBM显存容量|80 GB|192 GB (HBM3e)|2.4x|
|显存物理带宽|3.35 TB/s|8.0 TB/s|2.4x|

晶体管数量的物理堆叠直接决定了AI芯片的矩阵乘法吞吐量，但算力的最终释放受制于“内存墙”。B200集成了192GB的HBM3e（高带宽内存），以每秒8TB的速度搬运数据，相较于H100提升了2.4倍 1。在此生态中，技术标准（如HBM的堆叠层数与接口协议）完全由链主英伟达的GPU产品路线图绝对定义，上游存储厂商（如SK海力士、三星）在享受AI红利的同时，实际上已被无缝嵌合进链主的全球供应节奏中，丧失了产品定义的独立性 1。

### 产能与价值吞噬：CoWoS作为真正的物理瓶颈

市场表面叙事往往将HBM视为当前AI算力短缺的核心掣肘，但深入供应链的原子化审计表明，真正的“硬性物理瓶颈”并非存储芯片，而是台积电的CoWoS（Chip-on-Wafer-on-Substrate）先进封装产能 2。HBM是一个相对透明且易于预测的变量，存储厂商的产能爬坡和良率清晰可见；然而，CoWoS封装是将逻辑Die与HBM堆叠并集成到硅中介层上的关键物理步骤，处于产业链更深、更不透明的环节 2。如果没有CoWoS封装，即使是最先进的3nm或4nm晶圆也无法转化为可用的AI加速器 3。

在当前节点，该环节处于极度的“供给物理短缺”（绝对的卖方市场）。台积电管理层已明确表示，其CoWoS产能处于结构性超额认购状态，订单已排满至2025年甚至2026年深入期 3。尽管台积电正在激进扩产，预计到2026年底将产能从目前的每月7.5万至8万片晶圆提升至12万至13万片，但仅英伟达一家就预计将吞噬其中约60%的产能 3。这种算力垄断导致数据中心GPU的交货周期被拉长至36到52周，使得2026年中期下达的企业级订单被迫推迟至2027年第一季度才能交付 3。

产能的极度受限迫使产业链上下游寻找替代方案。由于台积电通常仅为自家代工的晶圆提供封装服务，为了突破这一封锁，SK海力士已开始转向英特尔（Intel）的EMIB（嵌入式多芯片互连桥接）技术寻求2.5D封装的替代产能 5。这一动向表明，在链主绝对垄断的压力下，供应链的物理外溢效应正在为具有深厚技术积累的替代厂商（如英特尔封装业务）创造巨大的“溢出红利” 6。

### 算力租赁破局：物理算力卡与客户粘性的博弈

算力物理短缺催生了GPU-as-a-Service（GPUaaS，GPU即服务）商业模式的指数级爆发。然而，对该赛道商业模式的穿透审计显示，行业内部存在着严重的分化：一部分沦为低毛利的套壳资金盘，而另一部分则成功构筑了深厚的利润护城河。

纯粹的“套壳资金盘”主要依赖于短期内的“拿卡能力”（即物理获取H100/A100的渠道）。这种模式本质上是硬件的低级套利，企业购买服务器后进行简单切分并按小时出租 7。随着时间推移、GPU制造产能逐步释放以及硬件代际更替（如Rubin架构的推出），这类缺乏技术附加值的“二房东”将迅速陷入内卷市场，利润率在大型云厂商（如AWS、Azure）的规模压制下被急剧压缩 8。

相反，以CoreWeave和Lambda Labs为代表的新型AI云提供商（Neoclouds），其核心护城河已远超单纯的物理算力卡，转变为以“基础设施粘性”和“技术服务栈”为核心的客户粘性 7。CoreWeave通过提供Kubernetes原生工具、裸金属（Bare-metal）直接访问（消除虚拟化开销）以及专门针对AI分布式训练优化的极速网络Fabric，显著缩短了客户的模型训练周期 7。一旦AI开发团队将其复杂的训练管线（Pipelines）和海量数据集部署在这些平台上，庞大的数据流出成本（Egress friction）和环境迁移风险将产生极高的转换成本 11。

通过绑定1到3年的长期预留合同，CoreWeave不仅锁定了未来的现金流，还实现了高达140%以上的净收入留存率（NRR） 11。这种模式证明，GPUaaS赛道的长期生存法则并非单纯的硬件堆砌，而是构建一层能够深度整合模型开发流程的AI原生软件中间件，从而在算力资本开支呈指数爆发的周期中，捕获超额的软件服务溢价 10。

## 互联与通信神经网瓶颈测算

当单芯片计算能力逼近极限时，集群互联网络便成为AI系统最致命的瓶颈。在动辄数万张GPU的集群中，网络通信的时延和带宽直接决定了算力的有效利用率。在这一赛道，铜线传输正在撞击不可逾越的物理红线，而光通信技术正在经历从封装形态到网络拓扑的彻底重构。

### 信号衰减墙与CPO/LPO的降噪突围

在网络接口从800G向1.6T乃至更高数据速率演进的进程中，传统的铜线传输已经彻底触及了物理极限的“信号衰减墙” 15。在112G和224G PAM4的高频信号传输中，由于电磁学的“趋肤效应”（Skin Effect），电流会极度集中在导体的最外层微米级表面运行 15。此时，任何微小的铜表面粗糙度都会导致信号传输路径的物理拉长，进而引发灾难性的插入损耗（Insertion Loss）和信号衰减 15。

为了在铜线上维持这种极高频率的信号，传统的可插拔光模块不得不依赖于极其耗电的数字信号处理芯片（oDSP）来对劣化的信号进行重新定时和深度补偿 16。这导致光模块的功耗急剧飙升，成为高密度机柜中的热力学定时炸弹 16。

为了突破这一红线，线性驱动可插拔光学器件（LPO）和光电共封装（CPO）技术应运而生 16。LPO架构通过直接移除功耗巨大的oDSP芯片，仅保留线性模拟组件（如具有均衡功能的激光驱动器和跨阻放大器 TIA），对光模块进行了深度降噪 16。据测算，LPO能将1.6T光模块的功耗削减至传统方案的三分之一，并将网络延迟压缩至纳秒级别，完美契合了AI算力网络对低延迟和低功耗的严苛要求 16。而CPO技术则更进一步，通过将光模块引擎与GPU/ASIC主芯片封装在同一基板上，将高频电信号的物理传输距离缩短至极限，从而在源头上规避了长距离铜线传输带来的信号损耗 16。

### 上下游时滞与EML激光器的“卡脖子”效应

在光互联产业链中，光芯片是技术壁垒最高的环节。审计发现，光通信环节的放量周期与上游英伟达（如Blackwell架构）的迭代周期严格同步甚至必须提前布局 17。在向1.6T演进的过程中，最大的“卡脖子”要素是电吸收调制激光器（EML）芯片 18。

对于1.6T光模块，单通道200G的EML激光器成为核心刚需，而其全球产能极度紧缺 19。高精度制造工艺（如光学对准）极大限制了规模化生产的扩张速度，导致200G EML的供给远落后于100G产品，维持了极高的定价权和市场溢价 18。据估计，2026年全球800G/1.6T光模块的需求量高达数千万只，对EML芯片的渴求呈现爆发式增长 19。这一时滞和产能瓶颈迫使业界开始加速研发硅光子学（Silicon Photonics）作为短期内的“泄压阀”，试图将更多功能集成到光子集成电路（PIC）中，以缓解对传统EML激光器的绝对依赖 17。

### 架构变异与节点不可替代性：OCS的全面接管

传统的数据中心网络架构依赖于电包交换机（EPS，Electrical Packet Switch），通过光电光（O-E-O）转换处理数据包 21。然而，在AI集群规模化下，EPS架构的功耗和拥塞问题已被放大至无法承受的地步。一组由64台基于机箱的Spine交换机组成的EPS网络，其耗电量竟高达1.9兆瓦 21。此外，数据包的存储与转发（Store-and-forward）不可避免地带来了微秒级的延迟和抖动，严重拖累了AI训练中各节点间的同步效率 21。

由此，光交叉连接（OCS，Optical Circuit Switch）技术正触发集群网络拓扑的深刻变异。OCS利用微机电系统（MEMS）的微镜阵列在自由空间内直接对光束进行物理重定向，实现了数据在光域内的纯粹透明传输，完全免除了O-E-O转换的功耗和延迟 21。OCS的引入并非仅仅是交换机的替换，而是实现了集群内无拥塞的物理直连，其协议无关性（Protocol-agnostic）和零缓冲（Zero buffering）特性，使其在算力网络中具有极强的“节点不可替代性” 21。

|   |   |   |
|---|---|---|
|架构特性|传统电包交换 (EPS)|光交叉连接 (OCS)|
|信号处理机制|光-电-光 (O-E-O) 转换|纯光域物理透明传输|
|网络延迟与抖动|微秒级，由缓存队列引发拥塞|纳秒级，无缓冲零抖动|
|功耗表现|极高 (由于芯片运算及DSP组件)|极低 (无OEO转换)|
|拓扑动态重构|静态，调整困难，节点故障影响大|动态物理路由，秒级故障旁路|
|应用案例代表|传统叶脊网络 (Leaf-Spine)|Google Palomar，NVIDIA Feynman|

以谷歌（Google）为例，其深度依赖自研的Palomar OCS架构，结合3D环面拓扑结构（3D Torus），能够将多达9216个TPU节点无缝连接 23。更重要的是，当某一个计算节点发生物理故障时，传统EPS网络的静态拓扑可能导致整个计算切片（Slice）的有效吞吐量暴跌至25%；而OCS通过动态光学重连，能够在物理层直接绕过故障节点，将系统的有效吞吐量维持在75%以上，极大地提升了系统的弹性和物理生存率 21。正是看到了这一终局，英伟达在规划其下一代“吉瓦级”AI工厂（Feynman架构）时，已明确将转向光学互联，并豪掷20亿美元与光通信巨头Lumentum签署战略合作，以锁定未来突破300端口限制的大规模OCS产能及技术标准 26。

## BOM底层材料与物理载体解构

剥离AI服务器的表面参数叙事，启动投入产出的原子化审计可以发现，GPU内部算力的每一次翻倍，都在强制要求最底层的PCB基板、铜箔、树脂甚至半导体制程气体进行极端的物理与化学性质换代。

### 物理层数爆发与单位面积价值的非对称提升

AI服务器主板（如GPU OAM加速模块和基板）与传统通用服务器相比，在结构复杂度和单价上呈现出非对称的指数级提升。通用服务器的主板层数通常在12至16层之间徘徊，而以NVIDIA DGX H100乃至GB200 NVL72为代表的AI训练服务器，其PCB层数被强制推升至20至30层的超高密度互连（HDI）结构 30。

这种层数的爆发并非简单的物理堆叠。由于GPU基板需要承载超过5000个BGA焊点的超高密度互连，传统的减成法制造工艺已无能为力，必须强制引入改良型半加成工艺（mSAP），将线宽/线距从传统的4/4 mil极限压缩至1.5/1.5 mil甚至更低 31。此外，为了满足极高频的传输需求，板材必须采用超低损耗（Ultra Low Loss）材料。这一系列的工艺与材料升级，导致AI服务器OAM PCB的制造成本飙升至每平方米约12,000元人民币，单位面积的附加值相比传统高多层板实现了数倍的跨越 30。

### 材料代际跃迁：M9树脂与超低轮廓铜箔

在数百G的传输速率下，PCB不再是简单的物理支撑载体，而是极度敏感的高频微波传输线。这一物理现实强制驱动了上游BOM材料的彻底换代。

首先是铜箔的微观形貌重构。前文提及的“趋肤效应”导致高频电流仅在铜箔表面流动 15。如果铜箔表面像山脉一样粗糙，电流的实际传播路径将被无限拉长，导致信号动能转化为热能消散 15。因此，AI算力板强制要求使用极低轮廓（VLP）乃至超极低轮廓（HVLP）铜箔，其表面粗糙度（Ra）必须被严格控制在0.15微米以下 15。这种高端铜箔原本由日本三井金属等企业垄断，但在AI需求的井喷下，成为了材料升级的绝对刚需 32。

其次是介质材料的代际跃迁。为了降低信号的介电损耗（Df）和介电常数（Dk），传统的环氧树脂已无法胜任，必须向PPO、PPE、BMI甚至PTFE等特种聚合物体系演进 32。随着英伟达Rubin架构的确立及其在2026年的量产预期，业内已确认将全面采用更先进的“M9级高速树脂 + HVLP3/4铜箔 + Q级电子布”方案 34。Q级电子布和M9树脂的技术壁垒极高，全球具备稳定量产能力的供应商屈指可数，重资产投入（单条Q fabric产线设备投资超5亿元）和长达18至24个月的建设周期，预示着该赛道将在2026年出现明确的“从0到1”的需求爆发和严重供需缺口 34。

### 供应链国产替代与TRL审计

在全球地缘政治与贸易保护主义抬头的背景下，高端材料与特种气体的国产替代（Local Substitution）已成为关乎产业链安全的战略核心。对国内厂商的技术成熟度等级（TRL，Technology Readiness Level）审计表明，中国企业正在快速捕获产能溢出效应。

在覆铜板（CCL）与高端基材领域，生益科技（SYTECH）等国内龙头已展现出极高的TRL水平。生益科技不仅突破了极低损耗（Ultra-Low Loss）材料的技术瓶颈，还针对AI服务器、毫米波雷达等领域推出了可量产的高阶材料，直接承接了因北美及台湾地区产能紧张而溢出的高端PCB订单 35。同时，铜冠铜箔、德福科技等国内铜箔企业也已快速切入HVLP铜箔供应链，打破了海外企业的长期垄断 32。

在半导体制造的基石——电子特种气体环节，国产替代的紧迫性更加凸显。随着3D NAND堆叠层数向300层以上演进以及逻辑芯片向亚5纳米节点突破，化学气相沉积（CVD）和腔室清洗对六氟化钨（WF6）和三氟化氮（NF3）的消耗量呈指数级增长 38。近期，受中国对关键战略矿产（如钨金属）出口管制的反向影响，日韩主导的WF6气体价格飙升了70%至90%，甚至引发了日系供应商可能断供的恐慌 39。在此节点，国内特气龙头如金宏气体（Jinhong Gas）展现了成熟的量产能力（高TRL），不仅成功与全球领先的存储芯片制造商签订了长期供气框架协议，还实现了海外市场的批量出口，吃透了全球供应链重构带来的“替代红利”与“产能溢价” 41。

## 热力学极限与算电基建重估

如果说芯片架构决定了AI的上限，那么热力学极限与电力基建则决定了AI的底线。“AI的尽头是电力”，这一论断在算电基建重估模型下得到了最残酷的验证。当前数据中心正面临着从散热介质到供电架构，再到微电网能源套利的全面重构。

### 热密度墙与冷却革命的强制转换

在传统数据中心内，空气冷却是绝对的主流。然而，空气的热容量和导热系数极低。通过热力学公式计算，使用空气带走1kW的热量，需要每分钟100立方英尺（CFM）的风量 43。当单机柜的功耗（TDP）突破40kW至41.3kW的“物理风冷极限”时，需要高达4,000 CFM的狂风穿过机柜 43。这不仅会产生高达95分贝的声学灾难，而且仅仅为了驱动风扇运转就需要消耗多达25kW的电力，使得PUE（电能利用效率）急剧恶化，导致热力学系统彻底崩溃 43。

随着AI芯片功耗的狂飙，当单机柜密度从8kW跃升至100kW，甚至向英伟达GB200 NVL72机柜及未来的500kW迈进时，液冷（包括冷板式和相变浸没式）从“可选项”被强制转变为不可违抗的“必选项” 43。水的单位体积热容量是空气的3300倍，仅需区区10加仑/分钟的温和水流即可轻松压制100kW的狂暴热量 43。

|   |   |   |
|---|---|---|
|冷却技术对比|传统风冷系统 (Air Cooling)|现代液冷系统 (Liquid Cooling)|
|单机柜TDP物理极限|~41.3 kW|100 kW 乃至更高 (无明确物理上限)|
|散热介质需求 (针对100kW)|10,000 CFM 气流 (理论值，实际已不可行)|10 GPM 液体流速|
|每兆瓦基础设施改造/建设成本|150万 - 200万美元|300万 - 400万美元|
|平均电能利用效率 (PUE)|1.4 - 1.8|1.05 - 1.15|
|硬件刷新生命周期 (Arrhenius定律)|3 - 4 年 (风扇轴承磨损、灰尘堆积)|5 - 7 年 (温度恒定，无机械风扇磨损)|

尽管液冷的初始资本开支（CAPEX）比风冷高出约一倍，但其能将PUE压低至1.05至1.15之间，符合欧洲（2030年PUE<1.3）及新加坡（PUE<1.2）的严苛合规要求 43。更重要的是，根据Arrhenius方程，设备工作温度每降低10摄氏度，电子元件的寿命将延长一倍 43。在这一赛道中，冷却核心部件的定价权牢牢掌握在能提供高可靠性冷却分配单元（CDU）、精密冷板流道设计以及两相浸没式特种氟化液的龙头企业手中，CDU单套系统的售价甚至高达15万美元 43。

### 供电架构突变：800V HVDC与垂直供电（VPD）

在算力中心内部，电力的输送路径正在经历深刻的削减与提效，旨在消除从电网到芯片（Grid-to-Chip）的每一瓦特无用功耗。

传统的供电架构依赖于多级交流电（AC）传输，庞大的中压变压器和低压交流配电网络在多次转换中积累了惊人的转换损耗和废热 45。为了解决这一问题，数据中心正在全面拥抱高压直流输电（HVDC）架构 46。例如，英伟达大力推行的800V HVDC架构，通过提高传输电压大幅降低了电流，从而极大地减少了铜缆的使用量和线路发热，为机架腾出了宝贵的物理空间，并将端到端电源效率提升了5%，维护成本削减了70% 46。

在这一供电突变中，基于碳化硅（SiC）的固态变压器（SST）成为了关键的“破局者”。目前全球电网基建面临严重瓶颈，传统铁芯中压变压器的交货周期已拉长至夸张的3年，成为AI工厂建设的致命硬伤 46。SST利用高压10kV SiC MOSFET等功率半导体件，直接将电网的中压交流电转换为800V直流电，省去了笨重的铁芯与绝缘油，不仅体积大幅缩小、模块化程度高，更将部署周期压缩至几个月，显著缓解了供应链危机 45。

而在芯片物理层面，垂直供电技术（VPD，Vertical Power Delivery）正在终结传统的横向供电方案 49。当AI芯片在1V以下的低电压工作并瞬间抽取数千安培电流时，即便是PCB板上最短的横向铜走线，也会因电阻产生不可忍受的 ![](data:image/png;base64,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) 功率损耗和压降 49。VPD通过将稳压器和定制硅电容器等无源器件直接植入封装基板内部或放置在主板背面正对芯片下方，实现了电力的“垂直灌入” 49。这不仅消除了寄生电阻，提升了系统对瞬态负载的响应速度，更释放了宝贵的基板正面空间，允许集成更多的HBM内存颗粒 50。

### 算电协同与AIDC的终局：能源套利护城河

面对动辄GW级别的庞大能耗，单纯依靠收取“机柜租赁费”的传统数据中心模式已经走向死胡同。Gartner报告指出，到2027年，全球财富500强企业预计将把高达5000亿美元的传统能源支出转移到微电网（Microgrids）建设上，以应对AI引发的电网崩溃危机和价格波动 54。AIDC（智算中心）运营商的长期物理生存率，将完全取决于其是否掌握了“能源套利能力”和“微电网调度权”。

在中国广袤的西部腹地（如宁夏腾格里沙漠基地），存在着海量的太阳能和风能。由于电网消纳能力有限，今年前两个月，中国光伏发电和风力发电的“弃电率”（被白白浪费的电能）分别飙升至9.2%和8.5% 55。前瞻性的AIDC运营商正在通过“绿电直连”和“源网荷储一体化”模式，直接在可再生能源基地旁建设微电网算力园区 44。通过大规模部署电池储能系统（BESS），这些AIDC不仅能以极低的成本获取原本将被遗弃的绿电，更能直接参与实时电力市场的能源套利（Energy Arbitrage） 59。

在加州独立系统运营商（CAISO）等电力现货市场中，智能的AIDC控制系统能够基于深度学习或混合整数非线性规划（MINLP）模型，动态预测未来几小时的电价 59。当电网产能过剩、电价跌至负值时，AIDC大量吸收绿电为其电池充电，并全功率运行AI训练任务；而当傍晚电网负荷达到峰值、电价飙升时，AIDC不仅可以降低算力负载，甚至能将电池中储存的廉价电力反向出售给公共电网，赚取高额差价 54。

这一套利过程并非毫无成本，电池的充放电循环会导致严重的容量衰减，研究表明，若不加控制，电池退化可能导致年度净利润下降13%至24% 60。因此，AIDC的核心护城河已经演变为一套极其复杂的“算电协同算法”——如何在AI训练任务的延迟容忍度、实时电价波动收益以及电池物理降解成本之间，找到最优的数学解 60。最终，在能源账单的达摩克利斯之剑下，成功的AIDC将不再被视为简单的房地产或IT租赁资产，而是成为具备强大计算能力的虚拟电厂（VPP），通过对电子和能源的双重物理操控，实现跨周期的永续盈利。

#### Works cited

1. H100 to B200: What Actually Changed | by AIQuest | Mar, 2026 ..., accessed May 11, 2026, [https://medium.com/@indiai/h100-to-b200-what-actually-changed-e652f9694daf](https://medium.com/@indiai/h100-to-b200-what-actually-changed-e652f9694daf)
    
2. CoWoS, Not HBM, Is the Real AI Supply Bottleneck | by elongated_musk - Medium, accessed May 11, 2026, [https://medium.com/@Elongated_musk/cowos-not-hbm-is-the-real-ai-supply-bottleneck-d0ae8f3f7ce4](https://medium.com/@Elongated_musk/cowos-not-hbm-is-the-real-ai-supply-bottleneck-d0ae8f3f7ce4)
    
3. The GPU Supply Chain Crisis: What Every Enterprise CIO Must ..., accessed May 11, 2026, [https://www.vamsitalkstech.com/ai/the-gpu-supply-chain-crisis-what-every-enterprise-cio-must-know-in-2026/](https://www.vamsitalkstech.com/ai/the-gpu-supply-chain-crisis-what-every-enterprise-cio-must-know-in-2026/)
    
4. Inside the AI Bottleneck: CoWoS, HBM, and 2–3nm Capacity Constraints Through 2027, accessed May 11, 2026, [https://info.fusionww.com/blog/inside-the-ai-bottleneck-cowos-hbm-and-2-3nm-capacity-constraints-through-2027](https://info.fusionww.com/blog/inside-the-ai-bottleneck-cowos-hbm-and-2-3nm-capacity-constraints-through-2027)
    
5. Intel's EMIB Challenges TSMC's CoWoS as America's Answer to the AI Packaging Bottleneck | SemiWiki, accessed May 11, 2026, [https://semiwiki.com/forum/threads/intel%E2%80%99s-emib-challenges-tsmc%E2%80%99s-cowos-as-america%E2%80%99s-answer-to-the-ai-packaging-bottleneck.24689/](https://semiwiki.com/forum/threads/intel%E2%80%99s-emib-challenges-tsmc%E2%80%99s-cowos-as-america%E2%80%99s-answer-to-the-ai-packaging-bottleneck.24689/)
    
6. SK hynix Turns to Intel's EMIB Packaging as TSMC CoWoS Bottlenecks Squeeze the AI Supply Chain - Wccftech, accessed May 11, 2026, [https://wccftech.com/sk-hynix-turns-to-intels-emib-packaging-as-tsmc-cowos-bottlenecks-squeeze-the-ai-supply-chain/](https://wccftech.com/sk-hynix-turns-to-intels-emib-packaging-as-tsmc-cowos-bottlenecks-squeeze-the-ai-supply-chain/)
    
7. GPU-as-a-Service Explained: The Business Model Behind AI, accessed May 11, 2026, [https://hashrateindex.com/blog/gpu-as-a-service-business-model-ai/](https://hashrateindex.com/blog/gpu-as-a-service-business-model-ai/)
    
8. GPU Marketplaces in 2026: How Aggregated Capacity Beats Hyperscalers | Spheron Blog, accessed May 11, 2026, [https://www.spheron.network/blog/top-gpu-rental/](https://www.spheron.network/blog/top-gpu-rental/)
    
9. Self-Hosted GPU or Model-as-a-Service? A Strategic Guide for AI Leaders - Alibaba Cloud, accessed May 11, 2026, [https://www.alibabacloud.com/blog/self-hosted-gpu-or-model-as-a-service-a-strategic-guide-for-ai-leaders_602930](https://www.alibabacloud.com/blog/self-hosted-gpu-or-model-as-a-service-a-strategic-guide-for-ai-leaders_602930)
    
10. Transforming GPU-as-a-Service into AI Cloud with Rafay - Techstrong.ai, accessed May 11, 2026, [https://techstrong.ai/sponsored-content/transforming-gpu-as-a-service-into-ai-cloud-with-rafay/](https://techstrong.ai/sponsored-content/transforming-gpu-as-a-service-into-ai-cloud-with-rafay/)
    
11. What is Customer Demographics and Target Market of CoreWeave Company?, accessed May 11, 2026, [https://businessmodelcanvastemplate.com/blogs/target-market/coreweave-target-market](https://businessmodelcanvastemplate.com/blogs/target-market/coreweave-target-market)
    
12. How Does CoreWeave Company Work? - Matrix BCG, accessed May 11, 2026, [https://matrixbcg.com/blogs/how-it-works/coreweave](https://matrixbcg.com/blogs/how-it-works/coreweave)
    
13. A Defining Year for The Essential Cloud for AI - CoreWeave, accessed May 11, 2026, [https://www.coreweave.com/blog/a-defining-year-for-the-essential-cloud-for-ai](https://www.coreweave.com/blog/a-defining-year-for-the-essential-cloud-for-ai)
    
14. GPU-as-a-Service for AI at scale: Practical strategies with Red Hat OpenShift AI, accessed May 11, 2026, [https://www.redhat.com/en/blog/gpu-service-ai-scale-practical-strategies-red-hat-openshift-ai](https://www.redhat.com/en/blog/gpu-service-ai-scale-practical-strategies-red-hat-openshift-ai)
    
15. How to Design PCBs for Data Centers and AI Servers - Sierra Circuits, accessed May 11, 2026, [https://www.protoexpress.com/blog/how-to-design-pcbs-for-data-centers-and-ai-servers/](https://www.protoexpress.com/blog/how-to-design-pcbs-for-data-centers-and-ai-servers/)
    
16. HUAWEI RESEARCH Issue 9, accessed May 11, 2026, [https://www-file.huawei.com/admin/asset/v1/pro/view/1f6f46557899427b9d6b37f0862a550d.pdf](https://www-file.huawei.com/admin/asset/v1/pro/view/1f6f46557899427b9d6b37f0862a550d.pdf)
    
17. "AI Silicon Photonics Chip" Related News - BigGo Finance, accessed May 11, 2026, [https://finance.biggo.com/s/AI%20Silicon%20Photonics%20Chip](https://finance.biggo.com/s/AI%20Silicon%20Photonics%20Chip)
    
18. AI optical transceiver market to reach $26b in 2026 - Compound Semiconductor, accessed May 11, 2026, [https://compoundsemiconductor.net/article/124045/AI_optical_transceiver_market_to_reach_26b_in_2026](https://compoundsemiconductor.net/article/124045/AI_optical_transceiver_market_to_reach_26b_in_2026)
    
19. Notes: Light is the Future (Pt.2) - Convequity, accessed May 11, 2026, [https://www.convequity.com/notes-light-is-the-future-pt-2/](https://www.convequity.com/notes-light-is-the-future-pt-2/)
    
20. InP Substrate: supply demand/ price hike sustainable/ key bottleneck, accessed May 11, 2026, [https://wukong123.substack.com/p/inp-substrate-supply-demand-price](https://wukong123.substack.com/p/inp-substrate-supply-demand-price)
    
21. OPTICAL CIRCUIT SWITCHING FOR AI AND HYPERSCALE ..., accessed May 11, 2026, [https://www.opencompute.org/documents/ocp-ocs-white-paper-april-2026-final-pdf](https://www.opencompute.org/documents/ocp-ocs-white-paper-april-2026-final-pdf)
    
22. Optical Circuit Switches | Lumentum, accessed May 11, 2026, [https://www.lumentum.com/en/products/data-center/optical-circuit-switches](https://www.lumentum.com/en/products/data-center/optical-circuit-switches)
    
23. Google TPU vs. NVIDIA GPU: Actual performance comes from system level, rather than chip level - YouTube, accessed May 11, 2026, [https://www.youtube.com/watch?v=G1arpj4y9A8](https://www.youtube.com/watch?v=G1arpj4y9A8)
    
24. TPUs vs. GPUs and why Google is positioned to win AI race in the long term - Hacker News, accessed May 11, 2026, [https://news.ycombinator.com/item?id=46069048](https://news.ycombinator.com/item?id=46069048)
    
25. Google's TPU vs Nvidia's GPU. @itsclivetime | by nothing but beautiful | MyVeryTech, accessed May 11, 2026, [https://medium.com/myverytech/googles-tpu-vs-nvidia-s-gpu-aeafd73f7bdb](https://medium.com/myverytech/googles-tpu-vs-nvidia-s-gpu-aeafd73f7bdb)
    
26. From Blackwell to Feynman: Analyzing NVIDIA's Optics Roadmap - Counterpoint Research, accessed May 11, 2026, [https://counterpointresearch.com/en/insights/from-blackwell-to-feynman-analyzing-nvidias-optics-roadmap](https://counterpointresearch.com/en/insights/from-blackwell-to-feynman-analyzing-nvidias-optics-roadmap)
    
27. Optical Circuit Switching for AI Data Centers - Molex, accessed May 11, 2026, [https://www.molex.com/en-us/blog/optical-circuit-switching-for-ai-data-centers](https://www.molex.com/en-us/blog/optical-circuit-switching-for-ai-data-centers)
    
28. NVIDIA Announces Strategic Partnership With Lumentum to Develop State-of-the-Art Optics Technology, accessed May 11, 2026, [https://nvidianews.nvidia.com/news/nvidia-announces-strategic-partnership-with-lumentum-to-develop-state-of-the-art-optics-technology](https://nvidianews.nvidia.com/news/nvidia-announces-strategic-partnership-with-lumentum-to-develop-state-of-the-art-optics-technology)
    
29. Bull of the Day: Lumentum (LITE) - Quartz, accessed May 11, 2026, [https://qz.com/bull-of-the-day-lumentum-lite](https://qz.com/bull-of-the-day-lumentum-lite)
    
30. Deconstructing AI Servers: A Look Inside PCB Composition and Value - aivon, accessed May 11, 2026, [https://www.aivon.com/blog/pcb-knowledge/deconstructing-ai-servers-a-look-inside-pcb-composition-and-value/](https://www.aivon.com/blog/pcb-knowledge/deconstructing-ai-servers-a-look-inside-pcb-composition-and-value/)
    
31. Technological Evolution of PCBs in the Era of Artificial Intelligence - Topfastpcb, accessed May 11, 2026, [https://www.topfastpcb.com/blog/technological-evolution-of-pcbs-in-the-era-of-artificial-intelligence/](https://www.topfastpcb.com/blog/technological-evolution-of-pcbs-in-the-era-of-artificial-intelligence/)
    
32. AI Server PCB Revolution: High-Frequency Materials & Market Trends 2026 - UGPCB, accessed May 11, 2026, [https://www.ugpcb.com/news/trade-news/ai-server-pcb/](https://www.ugpcb.com/news/trade-news/ai-server-pcb/)
    
33. High Frequency High Speed Copper Foil Market Outlook 2026-2034 - Intel Market Research, accessed May 11, 2026, [https://www.intelmarketresearch.com/high-frequencyhigh-speed-copper-foil-market-35958](https://www.intelmarketresearch.com/high-frequencyhigh-speed-copper-foil-market-35958)
    
34. M9, material upgrade confirmation! NVIDIA founder and CEO | 庚 ..., accessed May 11, 2026, [https://www.binance.com/en/square/post/33863485015834](https://www.binance.com/en/square/post/33863485015834)
    
35. Shengyi Technology USA – Manufacturer of Copper-Clad Laminates & Prepreg Materials for PCBs, accessed May 11, 2026, [https://www.shengyi-usa.com/](https://www.shengyi-usa.com/)
    
36. China Merchants Securities: AI Computing Power Remains the Main Theme, Focus on PCB Industry Chain Technology Iteration and Supply-Demand Gaps - Tiger Brokers, accessed May 11, 2026, [https://www.itiger.com/news/1191083750](https://www.itiger.com/news/1191083750)
    
37. Inside the AI Hardware Boom: Servers, Substrates and Advanced Packaging - I-Connect007, accessed May 11, 2026, [https://iconnect007.com/article/146416/inside-the-ai-hardware-boom-servers-substrates-and-advanced-packaging/146413/flex](https://iconnect007.com/article/146416/inside-the-ai-hardware-boom-servers-substrates-and-advanced-packaging/146413/flex)
    
38. Electronic Specialty Gases Market Research Report 2034 - Dataintelo, accessed May 11, 2026, [https://dataintelo.com/report/global-electronic-specialty-gases-market](https://dataintelo.com/report/global-electronic-specialty-gases-market)
    
39. [News] Peric Special Gases Drives China's Tungsten Gas Push Amid Memory Boom and Rival Price Hikes - TrendForce, accessed May 11, 2026, [https://www.trendforce.com/news/2026/03/12/news-peric-special-gases-drives-chinas-tungsten-gas-push-amid-memory-boom-and-rival-price-hikes/](https://www.trendforce.com/news/2026/03/12/news-peric-special-gases-drives-chinas-tungsten-gas-push-amid-memory-boom-and-rival-price-hikes/)
    
40. [News] Potential Supply Disruptions of Tungsten Hexafluoride from Japan: Implications for the Semiconductor Industry - TrendForce, accessed May 11, 2026, [https://www.trendforce.com/news/2026/04/08/news-potential-supply-disruptions-of-tungsten-hexafluoride-from-japan-implications-for-the-semiconductor-industry/](https://www.trendforce.com/news/2026/04/08/news-potential-supply-disruptions-of-tungsten-hexafluoride-from-japan-implications-for-the-semiconductor-industry/)
    
41. JinHong gas company released finanical report, accessed May 11, 2026, [https://en.igascn.com/chian/detail?TypeId=1026&Id=6186&SortSource=list](https://en.igascn.com/chian/detail?TypeId=1026&Id=6186&SortSource=list)
    
42. News - JinHong Gas, accessed May 11, 2026, [https://jh-gas.com/news/](https://jh-gas.com/news/)
    
43. Liquid Cooling vs Air Cooling for AI Data Centers | Introl Blog, accessed May 11, 2026, [https://introl.com/blog/liquid-vs-air-cooling-ai-data-centers](https://introl.com/blog/liquid-vs-air-cooling-ai-data-centers)
    
44. New Developments in AIDC Green Power Direct Connection Under the 80% 'Compute-Power Coordination' Threshold - Highjoule, accessed May 11, 2026, [https://www.highjoule.com/news/6542.html](https://www.highjoule.com/news/6542.html)
    
45. Rearchitecting Data Center Power for AI with Solid-State Transformers - Industry Articles, accessed May 11, 2026, [https://eepower.com/industry-articles/rearchitecting-data-center-power-for-ai-with-solid-state-transformers/](https://eepower.com/industry-articles/rearchitecting-data-center-power-for-ai-with-solid-state-transformers/)
    
46. Answering the call: Powering AI with reliable silicon ... - Wolfspeed, accessed May 11, 2026, [https://www.wolfspeed.com/knowledge-center/article/powering-ai-with-reliable-silicon-carbide-based-solid-state-transformers/](https://www.wolfspeed.com/knowledge-center/article/powering-ai-with-reliable-silicon-carbide-based-solid-state-transformers/)
    
47. Why HVDC and Solid State Transformers Matter for the Next Generation of AI Infrastructure, accessed May 11, 2026, [https://www.exascalelabs.ai/blog/why-hvdc-and-solid-state-transformers-matter-for-the-next-generation-of-ai-infrastructure](https://www.exascalelabs.ai/blog/why-hvdc-and-solid-state-transformers-matter-for-the-next-generation-of-ai-infrastructure)
    
48. Solid-state Transformers: A New Turning Point for Chip Manufacturers, accessed May 11, 2026, [https://eu.36kr.com/en/p/3799888201161990](https://eu.36kr.com/en/p/3799888201161990)
    
49. Embedded passives enhance vertical power delivery - EE World Online, accessed May 11, 2026, [https://www.eeworldonline.com/embedded-passives-enhance-vertical-power-delivery/](https://www.eeworldonline.com/embedded-passives-enhance-vertical-power-delivery/)
    
50. Vertical Power Delivery (VPD) solutions - Flex, accessed May 11, 2026, [https://flex.com/products/power-modules/vertical-power-delivery](https://flex.com/products/power-modules/vertical-power-delivery)
    
51. High-Current-Density Power Modules Mitigate the Environmental Impact of Power-Intensive GenAI - Vicor Corporation, accessed May 11, 2026, [https://www.vicorpower.com/resource-library/articles/high-performance-computing/modules-mitigate-the-environmental-impact-of-genai](https://www.vicorpower.com/resource-library/articles/high-performance-computing/modules-mitigate-the-environmental-impact-of-genai)
    
52. Empower Semiconductor Showcases Vertical Power Delivery Innovations at APEC 2026, accessed May 11, 2026, [https://www.empowersemi.com/empower-semiconductor-showcases-vertical-power-delivery-innovations-at-apec-2026/](https://www.empowersemi.com/empower-semiconductor-showcases-vertical-power-delivery-innovations-at-apec-2026/)
    
53. Vertical power delivery cuts energy loss in AI processor designs - Digital Watch Observatory, accessed May 11, 2026, [https://dig.watch/updates/vertical-power-delivery-cuts-energy-loss-in-ai-processor-designs](https://dig.watch/updates/vertical-power-delivery-cuts-energy-loss-in-ai-processor-designs)
    
54. Shifting $500 billion from energy costs to microgrid investments, accessed May 11, 2026, [https://canadiancor.com/shifting-500-billion-from-energy-costs-to-microgrid-investments/](https://canadiancor.com/shifting-500-billion-from-energy-costs-to-microgrid-investments/)
    
55. China's Wasting Too Much Renewable Power as Curtailments Rise - Energy Connects, accessed May 11, 2026, [https://www.energyconnects.com/news/renewables/2026/april/china-s-wasting-too-much-renewable-power-as-curtailments-rise/](https://www.energyconnects.com/news/renewables/2026/april/china-s-wasting-too-much-renewable-power-as-curtailments-rise/)
    
56. China sure-footed in carbon peak goals, accessed May 11, 2026, [https://www.chinadailyhk.com/hk/article/627049](https://www.chinadailyhk.com/hk/article/627049)
    
57. Strengthened coordination between computing and electricity ..., accessed May 11, 2026, [https://news.futunn.com/en/post/70573602/strengthened-coordination-between-computing-and-electricity-sectors-gains-policy-support](https://news.futunn.com/en/post/70573602/strengthened-coordination-between-computing-and-electricity-sectors-gains-policy-support)
    
58. In-depth analysis of the core logic and application value of the rising popularity of AIDC energy storage - EEWORLD, accessed May 11, 2026, [https://en.eeworld.com.cn/news/newenergy/eic714058.html](https://en.eeworld.com.cn/news/newenergy/eic714058.html)
    
59. Arbitrage Strategy of Renewable-Based Microgrids via Peer-to-Peer Energy-Trading - NTU > IRep, accessed May 11, 2026, [https://irep.ntu.ac.uk/id/eprint/48203/1/1639198_Vahidinasab.pdf](https://irep.ntu.ac.uk/id/eprint/48203/1/1639198_Vahidinasab.pdf)
    
60. Profitability of energy arbitrage net profit for grid-scale battery energy storage considering dynamic efficiency and degradation using a linear, mixed-integer linear, and mixed-integer non-linear optimization approach - ResearchGate, accessed May 11, 2026, [https://www.researchgate.net/publication/381434317_Profitability_of_energy_arbitrage_net_profit_for_grid-scale_battery_energy_storage_considering_dynamic_efficiency_and_degradation_using_a_linear_mixed-integer_linear_and_mixed-integer_non-linear_optim](https://www.researchgate.net/publication/381434317_Profitability_of_energy_arbitrage_net_profit_for_grid-scale_battery_energy_storage_considering_dynamic_efficiency_and_degradation_using_a_linear_mixed-integer_linear_and_mixed-integer_non-linear_optim)
    
61. Microgrid and energy arbitrage opportunities assessed | interest.co.nz, accessed May 11, 2026, [https://www.interest.co.nz/personal-finance/117797/small-communities-could-be-buying-selling-and-saving-money-electric-power](https://www.interest.co.nz/personal-finance/117797/small-communities-could-be-buying-selling-and-saving-money-electric-power)
    
62. Profitability of energy arbitrage net profit for grid-scale battery energy storage considering dynamic efficiency and degradatio - Politecnico di Torino, accessed May 11, 2026, [https://iris.polito.it/retrieve/efe6b4bf-a594-4a51-bc43-f623f7143f26/1-s2.0-S2352152X24019662-main.pdf](https://iris.polito.it/retrieve/efe6b4bf-a594-4a51-bc43-f623f7143f26/1-s2.0-S2352152X24019662-main.pdf)
    

**
