https://blog.csdn.net/AndrExpert/article/details/104328946

四个配置文件，四个步骤



### 多轮对话的总体流程
- NLU = 分类+实体识别
首先，将用户输入的Message传递到Interpreter(Rasa NLU模块)，

- 对话管理(DM) = DST + Policy

DST(dialog state tracking):对话状态维护
用数学形式表达为，t+1 时刻的对话状态S(t+1)，依赖于之前时刻 t 的状态St，和之前时刻 t 的系统行为At，以及当前时刻 t+1 对应的用户行为O(t+1)。S(t+1) ← St+At+O(t+1)
Policy: 动作候选**排序**

问答与多轮对话的不同点：
问答：　指代消解，query补全
多轮对话：决策过程：需要机器在对话过程中不断根据当前的状态决策下一步应该采取的最优动作

- action选择
第三，利用policy记录Tracker对象的当前状态，并选择执行相应的action，其中，这个action是被**记录**在Track对象中的；

- response
最后，将执行action返回的结果输出即完成一次人机交互。


### Rasa的架构
- Rasa NLU
该模块负责识别Message中的"意图(intent)“和提取所有"实体”(entity)数据；
- Rasa Core
Rasa Core是Rasa框架提供的对话管理模块，它类似于聊天机器人的大脑，主要的任务是维护更新对话状态和动作选择，然后对用户的输入作出响应。
Rasa Core会将Interpreter提取到的意图和识别传给Tracker对象，该对象的主要作用是跟踪会话状态(conversation state)；


### 训练数据
训练数据放在本项目data/目录下
Rasa框架提供了两种NLU模型训练样本数据格式，即Markdown或JSON，我们可以将NLU训练数据保存到单独的文件或者多个文件的目录。
- Rasa NLU的训练
nlu.md文件

#### 支持的任务
- 意图   intent --- sentences/words    文本与语义的映射关系
- 同义词  词库

- Rasa Core的训练
stories.md文件


### 配置文件
- config.yml
    配置NLU部分的各个子任务的算法,对话管理部分的policy
- credientials.yml
    其他服务(在本项目里是一个flask server)访问Rasa Server时，在该文件中配置相关信息。
- endpoints.yml
    Rasa Server访问其他服务的时候的配置
- domain.yml
    定义action
    记录了系统所有的信息

当Rasa NLU识别到用户输入Message的意图后，Rasa Core对话管理模块就会对其作出回应，而完成这个回应的模块就是action。
Rasa Core支持三种action，即default actions、utter actions以及 custom action(自定义action)

在domain.yml文件中定义查询天气和空气质量的action

### NLU组件

### 对话管理组件



Slots的定义位于domain.yaml文件中，它们通常与Entities相对应，即Entities有哪些，Slots就有哪些，并且Slots存储的值就是NLU模型提取的Entities的值。

### 实践一般流程
- 模型训练：
python3 -m rasa train --config configs/config.yml --domain configs/domain.yml --data data/

- 启动rasa服务
该服务实现自然语言理解(NLU)和对话管理(Core)功能
注：该服务的--port默认为5005，如果使用默认则可以省略
python3 -m rasa run --port 5005 --endpoints configs/endpoints.yml --credentials configs/credentials.yml --debug

- 启动action服务
注：该服务的--port默认为5055，如果使用默认则可以省略
python3 -m rasa run actions --port 5055 --actions actions --debug

- 启动自己的服务
python3 first_server.py

### 依赖安装
- 安装rasa
pip3 install rasa

- 安装MITIE
MITIE是在dlib机器学习库之上开发的NLP工具包，支持分布式词嵌入和结构化SVM。提供英语，西班牙语，德语的预训练语言模型。MITIT核心代码使用C++编写，支持Python，R，Java,C,MATLAB的集成。

安装MITIE：
git clone https://github.com/mit-nlp/MITIE.git
python setup.py build
python setup.py install

- 安装web框架
pip3 install flask




使用Facebook的Duckling实现基于规则的实体识别：DucklingHTTPExtractor




### Rasa X
Rasa X提供了UI界面用于交互式学习


以md和json组织,管理数据/语料的方式，只能放在本地??
组件化的架构，适合对于多轮对话这种复杂的涉及多种算法的任务



utter
adj.	完全的; 十足的; 彻底的;
v.	出声; 说; 讲;

affirm
v.	肯定属实; 申明; 断言;






