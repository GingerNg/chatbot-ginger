https://blog.csdn.net/AndrExpert/article/details/104328946

- 首先，将用户输入的Message传递到Interpreter(Rasa NLU模块)，该模块负责识别Message中的"意图(intent)“和提取所有"实体”(entity)数据；

- 其次，Rasa Core会将Interpreter提取到的意图和识别传给Tracker对象，该对象的主要作用是跟踪会话状态(conversation state)；
- 第三，利用policy记录Tracker对象的当前状态，并选择执行相应的action，其中，这个action是被**记录**在Track对象中的；
- 最后，将执行action返回的结果输出即完成一次人机交互。


python3 -m rasa train --config configs/config.yml --domain configs/domain.yml --data data/


当Rasa NLU识别到用户输入Message的意图后，Rasa Core对话管理模块就会对其作出回应，而完成这个回应的模块就是action。Rasa Core支持三种action，即default actions、utter actions以及 custom action



MITIE
MITIE是在dlib机器学习库之上开发的NLP工具包，支持分布式词嵌入和结构化SVM。提供英语，西班牙语，德语的预训练语言模型。MITIT核心代码使用C++编写，支持Python，R，Java,C,MATLAB的集成。

安装MITIE：
git clone https://github.com/mit-nlp/MITIE.git
python setup.py build
python setup.py install


Rasa框架提供了两种NLU模型训练样本数据格式，即Markdown或JSON，我们可以将NLU训练数据保存到单独的文件或者多个文件的目录。


使用Facebook的Duckling实现基于规则的实体识别：DucklingHTTPExtractor



















