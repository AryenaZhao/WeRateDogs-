# WeRateDogs-
## 总述
该项目是udacity学堂中数据分析进阶课程的数据清洗项目，我们从WeRateDogs博主的推特博客上下载相应的狗狗的推特档案，推特图像的预测数据，以及每条推特的额外附加数据，在项目中对数据进行评估，清洗以及存储分析。

## 我们需要什么软件
* 你需要在电脑上用 Jupyter Notebook 操作。
* 需要安装下列软件包（即 Python 库）。你可以通过 conda 或 pip 安装这些库。
pandas
numpy
requests
tweepy
json
* 你需要创建包含图片的书面文档，并且把这些文档导出为 PDF 文件。这个任务可以在 Jupyter Notebook 中进行，但是最好使用文字处理软件，如免费软件 Google Docs 或 Microsoft Word。
* 文本编辑器，如免费软件 Sublime，这可能会用到，但不是必须的。

## 关键要点
清洗这个项目的数据时要牢记几个要点：
* 我们只需要含有图片的原始评级 (不包括转发)。尽管数据集中有 5000 多条数据，但是并不是所有都是狗狗评分，并且其中有一些是转发。
* 完整地评估和清理整个数据集将需要大量时间，实践和展示数据处理技巧没有必要将这个数据集全部清理。因此，本项目的要求只是评估和清理此数据集中的至少 8 个质量问题和至少 2 个整洁度问题。
* 根据 整洁数据 tidy data 的规则要求，本项目的数据清理应该包括将三个数据片段进行合并。
* 如果分子评级超过分母评级，不需要进行清洗。这个 特殊评分系统 是 WeRateDogs 人气度较高的主要原因。（同样，也不需要删除分子小于分母的数据）
* 不必收集 2017 年 8 月 1 日之后的数据，你可以收集到这些推特的基本信息，但是你不能收集到这些推特对应的图像预测数据，因为你没有图像预测算法的使用权限。

## 数据介绍
### 评分介绍
WeRateDogs 是一个推特主，他以诙谐幽默的方式对人们的宠物狗评分。这些评分通常以 10 作为分母。但是分子则一般大于 10：11/10、12/10、13/10 等等。
### 狗狗的地位等级
根据狗狗的年纪以及大小，将狗狗评定为的不同地位 (stage): doggo, pupper, puppo, 和 floof(er) (摘自 Amazon 上的 #WeRateDogs book)，这种地位往往在数据的text中体现，不需要我们根据原始数据进行分类，只需要从text中提取即可。
### 图像预测文件字段解释
* tweet_id 是推特链接的最后一部分，位于 "status/" 后面 → https://twitter.com/dog_rates/status/889531135344209921
* jpg_url 是预测的图像资源链接
* img_num 最可信的预测结果对应的图像编号 → 1 推特中的第一张图片
* p1 是算法对推特中图片的一号预测 → 金毛犬
* p1_conf 是算法的一号预测的可信度 → 95%
* p1_dog 是一号预测该图片是否属于“狗”（有可能是其他物种，比如熊、马等） → True 真
* p2 是算法对推特中图片预测的第二种可能性 → 拉布拉多犬
* p2_conf 是算法的二号预测的可信度 → 1%
* p2_dog 是二号预测该图片是否属于“狗” → True 真
* 以此类推...

## 项目细节
你在这个项目中的任务如下：
数据整理，其中包括：
* 收集数据
* 评估数据
* 清洗数据
对清洗过的数据进行储存、分析和可视化
书面报告 1) 你的数据整理工作 和 2) 你的数据分析和可视化
### 对项目数据进行收集
在名字为 wrangle_act.ipynb 的 Jupyter Notebook 中收集下面所述的三份数据：
* WeRateDogs 的推特档案。这个数据文件是直接提供给你的，所以你可以将其当作是“资料来源：手头文件”来收集（参见课程 2：收集数据）。文件会放在文件库中
* 推特图像的预测数据，即根据神经网络，对出现在每个推特中狗的品种（或其他物体、动物等）进行预测的结果。这个文件你需要使用 Python 的 Requests 库和以下提供的 URL 来进行编程下载。下载用的 URL：https://raw.githubusercontent.com/udacity/new-dand-advanced-china/master/%E6%95%B0%E6%8D%AE%E6%B8%85%E6%B4%97/WeRateDogs%E9%A1%B9%E7%9B%AE/image-predictions.tsv 。
* 每条推特的额外附加数据，至少要包含转发数（retweet_count）和喜欢数（favorite_count），还可以收集任何你觉得有趣的字段。使用 WeRateDogs 推特档案中的推特 ID，使用 Python Tweepy 库查询 API 中每个推特的 JSON 数据，把所有 JSON 数据存储到一个名为 tweet_json.txt 的文件中。每个推特的 JSON 数据应当写入单独一行。然后将这个 .txt 文件逐行读入一个 pandas DataFrame 中，至少包含 tweet ID、retweet_count 和 favorite_count 字段。注：不要在项目提交中包含你的推特 API 密钥和访问令牌（可以用 `` 号代替）*。
### 对项目数据进行评估
收集上述三个数据集之后，使用目测评估和编程评估的方式，对数据进行质量和清洁度的评估。在你的 wrangle_act.ipynb Jupyter Notebook 中记录评估过程和结果，最终列出至少 8 个质量问题 和 2 个清洁度问题。要符合项目规范，必须对项目动机中的要求进行评估（参见上一页课程的 关键要点 标题）。
### 对项目数据进行清洗
对你在评估时列出的每个问题进行清洗。在 wrangle_act.ipynb 展示清洗的过程。结果应该为一个优质干净整洁的主数据集（pandas DataFrame 类型） （如果都是以推特 ID 为观察对象的一些特征列，则清理最终只能有一个主数据集，如果有其他观察对象及其对应的特征字段，可以创建其他的数据集，同样需要清理）。同样地，必须符合项目动机的要点要求。
### 对项目数据进行存储、分析和可视化
将清理后的数据集存储到 CSV 文件中，命名为 twitter_archive_master.csv。如果有其他观察对象的数据集存在，需要多个表格，那么要给这些文件合理命名。另外，你也可以把清洗后的数据存储在 SQLite 数据库中（如果这样存储的话，该数据库文件也需要提交）。
在 wrangle_act.ipynb Jupyter Notebook 中对清洗后的数据进行分析和可视化。必须生成至少 3 个见解和 1 个可视化。
### 项目汇报
创建一个 300-600 字的书面报告，命名为 wrangle_report.pdf，在该报告中简要描述你的数据整理过程。这份报告可以看作是一份内部文档，供你的团队成员查看交流。
创建一个 250 字以上的书面报告，命名为 act_report.pdf，在该报告中，你可以与读者交流观点，展示你使用整理过的数据生成的可视化图表。这份报告可以看作是一份外部文档，如博客帖子或杂志文章。
这两个报告都可以使用 Jupyter Notebook 中的 Markdown 功能进行创建，然后以 PDF 格式下载（见下图）。不过你可能更倾向于使用文字处理软件，如 Google Docs 或 Microsoft Word，因为这两份报告 并不包含代码，使用文字处理软件更加便捷。

## 项目重难点介绍
本项目主要是采用数据清理的技术，采用的重点是从HTTP和json中获取数据，以及使用正则表达式整理数据，以及循环的使用。

## ToDo
数据中大量信息话没有完全提取出来，后期希望能够进一步学习正则，更进一步的提取信息。
