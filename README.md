https://blog.csdn.net/AndrExpert/article/details/104328946

- 首先，将用户输入的Message传递到Interpreter(Rasa NLU模块)，该模块负责识别Message中的"意图(intent)“和提取所有"实体”(entity)数据；

- 其次，Rasa Core会将Interpreter提取到的意图和识别传给Tracker对象，该对象的主要作用是跟踪会话状态(conversation state)；
- 第三，利用policy记录Tracker对象的当前状态，并选择执行相应的action，其中，这个action是被**记录**在Track对象中的；
- 最后，将执行action返回的结果输出即完成一次人机交互。

当Rasa NLU识别到用户输入Message的意图后，Rasa Core对话管理模块就会对其作出回应，而完成这个回应的模块就是action。
Rasa Core支持三种action，即default actions、utter actions以及 custom action(自定义action)

在domain.yml文件中定义查询天气和空气质量的action

对话管理
问答：　指代消解，query补全
多轮对话：决策过程：需要机器在对话过程中不断根据当前的状态决策下一步应该采取的最优动作
DST(dialog state tracking):对话状态维护
Policy: 动作候选**排序**

Slots的定义位于domain.yaml文件中，它们通常与Entities相对应，即Entities有哪些，Slots就有哪些，并且Slots存储的值就是NLU模型提取的Entities的值。

- 模型训练：
python3 -m rasa train --config configs/config.yml --domain configs/domain.yml --data data/

- 启动rasa服务
该服务实现自然语言理解(NLU)和对话管理(Core)功能
注：该服务的--port默认为5005，如果使用默认则可以省略
python3 -m rasa run --port 5005 --endpoints configs/endpoints.yml --credentials configs/credentials.yml --debug

- 启动action服务
注：该服务的--port默认为5055，如果使用默认则可以省略
python3 -m rasa run actions --port 5055 --actions actions --debug


python3 first_server.py

MITIE
MITIE是在dlib机器学习库之上开发的NLP工具包，支持分布式词嵌入和结构化SVM。提供英语，西班牙语，德语的预训练语言模型。MITIT核心代码使用C++编写，支持Python，R，Java,C,MATLAB的集成。

安装MITIE：
git clone https://github.com/mit-nlp/MITIE.git
python setup.py build
python setup.py install


Rasa框架提供了两种NLU模型训练样本数据格式，即Markdown或JSON，我们可以将NLU训练数据保存到单独的文件或者多个文件的目录。


使用Facebook的Duckling实现基于规则的实体识别：DucklingHTTPExtractor




### Rasa X
Rasa X提供了UI界面用于交互式学习












