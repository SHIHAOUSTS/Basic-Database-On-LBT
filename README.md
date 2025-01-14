# Basic-Database-On-LBT
欢迎！此仓库主要储存执行Ladybug、Honeybee-Energy、Honeybee-Radiance、Dragonfly时必不可少的可复用参数信息。  

它可以是 Program Type、Loads、Schedule、Construction-Set、Construction、Modifie Set 以及 Modifie 等复用率较高的内容。也可以是明确了来源和具体使用范围的气象数据文件（.EPW File）及设计日文件（.DDY File）。

目前，更新主要以Program Type为主，并拆分Loads与Schedule分发至其他文件下。Construction-Set、Construction会随机更新，这取决于鄙人怨种妹妹的工作热情，不可催。

# 1  前言

在建筑节能设计中，如果根据不同地区的气候条件进行合理的节能设计，则可以有效地提高建筑能效，减少能源消耗，所以不同的地区会采用不同的节能措施，并且对于相关节能技术的主要技术指标，不同地区标准中的参考和限定数值也会有所不同。例如，寒冷地区的气温较低，采暖季较长，节能设计侧重点也是保温隔热、冬季供暖以及减少能源消耗，建筑需要采用高效保温材料、采暖设备的效率要求高等等，所以在相关地区的节能设计规范或标注中，建筑围护的传热系数规定通常会以一个较低的数值进行限制，以达到最低限度的建筑节能需求。

我国现行的国家及地方节能设计规范众多，以《公共建筑节能设计标准》GB50189-2015的规定作为参考，建筑节能气候分区主要划分为严寒、寒冷、夏热冬冷、夏热冬暖以及温和地区5个区域。其中又因我国各省份幅员辽阔，同一地区的气候可能会出现些许差别，故又在5个节能气候分区的基础上又分为A、B、C区。不仅如此，对于不同的建筑，对节能设计的要求与侧重点也是不一样的。例如在节能设计中，通常将建筑的类型分为居住建筑、公共建筑和工业建筑三大类，每一种类型的建筑都又会有独立的要求。

由于这些因素，导致我国的节能设计规范、标准以及相关指导文件五花八门，能让人眼花缭乱，沉没在信息的海洋，也导致了行业模块化、数字化的标准化信息得不到有效的搜集，对于更能够利用新技术充当效率武器的绿色建筑与节能工程师来说，在工作的进程中如没有长时间的积累，重复的工作和枯燥的信息搜集工作会降低工程师的工作幸福感。

近年，正在开展行业规范的瘦身行动，例如在现行的《建筑节能与可再生能源利用通用规范》GB55015-2021中，统一规范了各建筑类型在不同建筑节能气候分区下的围护结构热工性能等信息，进一步集中并废止了此前了五花八门的部分标准规定。

可以通过行业变革的这个契机，通过Ladybug Tools这个模块化、参数化的工具来进行标准化的信息搜集，并通过开源的形式公布给所有行业的学生、教师、工程师等，促进行业的交流以及信息化的发展。

# 2  一些痛点

这是个很艰难但很有意义的事情，但是在执行过程中会出现很多千奇百怪的事情,例如：

- 目前仍有部分地区在外窗相关的节能设计规定中，遮阳系数（SC）和太阳得热系数(SHGC)同时使用，并分冬夏两季节有不同规定，目前我没想到很好的办法去解决这个问题，所以Construction与Construction Set的内容一直在搁置状态。

- 并非所有地区都有现成的设计日数据文件，例如我国。虽然国外开放的气象数据下载站点中，气象数据的文件往往包含着DDY文件，国内的开放气象数据也会包含这些DDY文件，但是细心的用户会发现，这些DDY文件中记录的数据并不符合国内的标准，所以国内的用户则不能很好的体会到这方面的便利。原因可从《民用建筑供暖通风与空气调节设计规范》GB 50736 - 2012 4.1.1 室外空气计算参数的条文说明中找到答案：

  > 我国使用的室外空气计算参数确定方法与国外不同，一般是按平均或累年不保证日（时）数确定，而美国、日本及英国等国家一般采用不保证率的方法，计算参数并不唯一，选择空间较大。经过专题研究，虽然国外的方法更灵活，能够针对目标建筑做出不同的选择，但我国的观测设备条件有限，目前还不能够提供所有主要城市30年的逐时原始数据，用一日四次的定时数据计算不保证率的结果与逐时数据的结果是有偏差的；而且从我国第一本暖通规范《工业企业供暖通风和空气调节设计规范》TJ 19出版以来一直沿用此种方法，广大的设计工作者已经习惯于这种传统的格式。
  >
  > 随着我国经济发展，超高层建筑不断增多，高度不断增加，超高层建筑上部风速、温度等参数与地面相比有较大变化，应根据实际高度，对室外空气计算参数进行修正。
  >
  > ——————————《民用建筑供暖通风与空气调节设计规范》GB 50736 - 2012 4.1.1 室外空气计算参数

  十年过去了，不管是观测设备、科学发展水平和社会经济水平都有了显著的提高，但仍未有相关的数据库数据做了对应更新，很难高效进行数字化文件的编辑，至少我做了几个DDY文件，从流程上看，非常累人。

- 部分地区在不透明围护结构（如外墙、屋面）相关的节能设计规定中，会考虑建筑所用材料的蓄热能力，并使用构造的蓄热系数作为外围护结构热工性能参考值的判定指标。但在E+中，我们设置的材料物性中并不包含蓄热系数，这使得使用Ladybug Tools制作具有显著区分材料的工作量可能会大大增加。
- 规范太多、导则太杂、指导文件信息化极为落后，这些东西阻碍着生产力的提高，但又不得不一直忍受这种现状。
- 其他没讲到的地方

希望大家能从这些痛点分享中体会到该仓库的珍贵。

# 3  预计更新计划

由于我个人经历和能力有限，所以目前仅承诺在空闲时间中更新如下内容，如更新完毕会用删除线标明：

- [x] ~~符合《建筑节能与可再生能源利用通用规范》GB55015-2021 附录 C 的 Program Type~~
- [x] ~~符合《民用建筑绿色性能计算标准》JGJ/T 449-2018 附录 C 的 Program Type（除居住建筑）~~
- [x] ~~符合《建筑围护结构节能工程做法及数据》09J908-3 的标准做法的 Construction（大部分，鄙人数据库资源有限）~~
- [x] ~~建筑门窗节能性能标识网中标识产品目录中的提供节能门窗参数，按U值、SHGC值以及标签序号排列（详尽名称无法填写，允许字符有限）~~
- [ ] 符合《近零能耗建筑技术标准》GB/T 51350-2019 附录 A 的 Program Type

期望有人和我来进行这些内容的补充，欢迎在Issue中讨论如何做这些内容：

- [ ] 符合《建筑围护结构节能工程做法及数据》09J908-3 的标准做法的 Construction（目前已完成了大部分，但材料中的热吸收系数、太阳辐射吸收系数和可见光辐射吸收系数、粗糙度等内容期望有缘人来更新）
- [ ] 符合《民用建筑供暖通风与空气调节设计规范》GB 50736-2012 的 Design Day
- [ ] 符合《建筑节能与可再生能源利用通用规范》GB55015-2021 3.1 建筑和围护结构规定的 Construction Set

# 4  如何使用这个库中分享的文件？

## 4.1  通过本地标准库直接调用（推荐）

每个Ladybug Tools程序安装后都会有基本库和用户库两种本地标准库文件夹，较新版本的Ladybug Tools和Pollination用户的本地标准库文件应在如下路径中：

`C:\Users\[Username]\AppData\Roaming\ladybug_tools\standards`

![image](https://github.com/GudaoStudio/Basic-Database-On-LBT/assets/51848364/5575bb35-3c18-464c-8568-4fbbe2ad30f1)


用户可以将库中的文件拉取至本地后放入`standards`目录下的对应子目录中，重新启动Rhino及Grasshooper，即可通过文本输入（需要名称完备）或通过HB Search相关组件输入关键词搜索调用（强烈推荐！）。

![image](https://github.com/GudaoStudio/Basic-Database-On-LBT/assets/51848364/7078bd8e-d510-4358-a0a8-750e723ed97a)


## 4.2  通过本地加载库文件进行调用

由于库中文件均是符合Honeybee文件标准的.hbjson文件，所以可以通过HB Load Objects 组件通过给定Honeybee File路径的形式进行读取使用。

![image](https://github.com/GudaoStudio/Basic-Database-On-LBT/assets/51848364/2d32ee07-8fde-452c-b8c7-0f138e87b5fd)


## 4.3  通过复制字符串进行调用

如果特别懒，或不会下载文件的用户（真的有）。可以使用 HB String To Object 组件通过在Panel中粘贴仓库中公开的代码来获得HB Objects。但是Grasshopper中，在Panel中的直接复制粘贴有行数限制，如果超出限制则会被截断，导致数据丢失。此法仅小案例应急用。

![image](https://github.com/GudaoStudio/Basic-Database-On-LBT/assets/51848364/3822a633-d1a5-43a6-a065-3640575def34)


# 5 如何参与这个库的维护

维护这个库可以通过发PR(Pull requests)，提 Issues 和群聊互动几个渠道参与库的维护。

## 5.1  提issue
1.注册 Github 账户

2.在 Basic-Database-On-LBT 项目仓库中的左上角点击Issues。

3.在Issues界面的右上角点击 New Issue。

4.填写你遇到的问题或想交流的问题乃至你想要我为你做的事情（如果我能力足够且精力允许）

5.点击Submit new issue 发送Issues，此时这个问题会像一个正式的帖子一样被所有人浏览。

## 5.2  Pull requests
1.注册 Github 账户

2.Fork Basic-Database-On-LBT 项目中的内容，同时可以使用 Git 或者 Github Desktop 克隆仓库中的内容到本地并建立同步。

3.使用任意顺手的编辑器直接修改源文件 或 使用HB Dump Objects的组件将任意HB Object翻译成JSON文件并放置于仓库的本地文件夹中（当然，这可以是任意符合该仓库需要的东西）。

4.使用 Git 命令或者 Github Desktop填写 Commit Message，并进行Pull requests提交你的修改或贡献。

5.等待审核，审核通过后我会进行合并，届时可以在主库中查看您的修改与贡献。

注意：一般情况下审核者会是我，只要你能写清楚你提交的东西是什么，我不在乎你写的是中文还是英文


## 5.3  群聊互动
登录Fly！Ladybug&Honeybee 的交流QQ群或微信群，向我提出你的疑问或问题（切勿@我）

QQ群号：817688321 

微信群：QQ群中不定时公布二维码

Discord：日程计划中......

# 6 已知但无法解决的问题

## 6.1  游泳馆冬季设定温度大于夏季设定温度
《民用建筑绿色性能计算标准》JGJ/T 449-2018 附录 C 第60页出现了冬季设定温度大于夏季设定温度的情况，该情况会造成Energyplus计算失败，且不能通过标准化的 Program Type 进行修正。
![image](https://github.com/GudaoStudio/Basic-Database-On-LBT/assets/51848364/41f6cb7f-9158-4edf-a9a1-337728e95182)
