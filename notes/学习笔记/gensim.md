# Gensim

Gensim 是一个开源的 Python 库，用于从原始的非结构化的文本中，无监督地学习到文本潜在的主题向量表达。除了具备基本的预料处理功能外，Gensim 还支持包括 TF-IDF，LSA，LDA，和 word2vec 在内的多种主题模型算法，支持流式训练（online training），并提供了诸如相似度计算，信息检索等一些常用任务的 API 接口。  

<!-- GFM-TOC -->
* [基本概念](#基本概念)
* [训练语料的预处理](#训练语料的预处理)
    * [预处理过程](#预处理过程)
    * [Corpus Streaming 流式处理](#Corpus Streaming 流式处理)
* [主题向量的变换](#主题向量的变换)
<!-- GFM-TOC -->

## 基本概念
### Corpus
Corpus(语料) 也称为训练语料库，是一组原始文本的集合，是 Gensim 的输入，用于无监督的训练文本主题的潜在结构。从语料中推断出的潜在结构，可以用来对一个新的文档指定一个主题。训练过程不需要人工干预，主题分类是无监督的。

### Vector
在 VSM (Vector Space Model) 中，每个文档都由一组特征表示。

### Sparse Vector
稀疏向量：我们可以略去向量中多余的0元素。此时，向量中的每一个元素是一个 (key, value) 的 tuple。

### Model
在向量化了语料之后，可以使用各种模型。模型 Model 指的是一个文档表示到另一个文档表示的转换。在 Gensim 中，文档用向量来表示，所以模型可以认为是在两个向量空间进行转换。这个转换是从训练语料库中学习出来的。

## 训练语料的预处理
训练语料的预处理指的是将文档中原始的字符文本转换成Gensim模型所能理解的稀疏向量的过程。  

### 预处理过程
1. 首先需要对原始预料进行分词和去停用词操作，在预料中一行对应着一个文档。
```python
texts = [['human', 'interface', 'computer'],
 ['survey', 'user', 'computer', 'system', 'response', 'time'],
 ['eps', 'user', 'interface', 'system'],
 ['system', 'human', 'system', 'eps'],
 ['user', 'response', 'time'],
 ['trees'],
 ['graph', 'trees'],
 ['graph', 'minors', 'trees'],
 ['graph', 'minors', 'survey']]
```

2. 在正式处理之前，我们想对语料中的每一个单词关联一个唯一的 ID。这可以用 gensim.corpora.Dictionary 来实现。这个字典定义了我们要处理的所有单词表。
```python
>>> from gensim import corpora
>>> dictionary = corpora.Dictionary(texts)
>>> dictionary.save('/tmp/deerwester.dict')  # store the dictionary, for future reference
>>> print(dictionary.token2id)
{'minors': 11, 'graph': 10, 'system': 5, 'trees': 9, 'eps': 8, 'computer': 0,
'survey': 4, 'user': 7, 'human': 1, 'time': 6, 'interface': 2, 'response': 3}
```

3. 采用 bag-of-words（词袋模型）将每个文档表示为一个稀疏向量。使用 dictionary 中的 doc2bow 方法来获得词袋向量表达。向量中的每一个元素是一个 (key, value), key 代表 dictionary 中的词，value 是该词在该篇文档中出现的次数。
```python
>>> corpus = [dictionary.doc2bow(text) for text in texts]
>>> corpora.MmCorpus.serialize('/tmp/deerwester.mm', corpus)  # store to disk, for later use
>>> print(corpus)
[(0, 1), (1, 1), (2, 1)]
[(0, 1), (3, 1), (4, 1), (5, 1), (6, 1), (7, 1)]
[(2, 1), (5, 1), (7, 1), (8, 1)]
[(1, 1), (5, 2), (8, 1)]
[(3, 1), (6, 1), (7, 1)]
[(9, 1)]
[(9, 1), (10, 1)]
[(9, 1), (10, 1), (11, 1)]
[(4, 1), (10, 1), (11, 1)]
```

到这里，训练语料的预处理工作就完成了。我们得到了语料中每一篇文档对应的稀疏向量（这里是 bow 向量）；向量的每一个元素代表了一个 word 在这篇文档中出现的次数。值得注意的是，虽然词袋模型是很多主题模型的基本假设，这里介绍的 doc2bow 函数并不是将文本转化成稀疏向量的唯一途径。

### Corpus Streaming 流式处理
由上述方法得到的 corpus 以 python list 的形式存在内存中，但在实际应用中有数百万个文档，全部存在 RAM 中不可行。因此出于内存优化的考虑，Gensim 支持文档的流式处理。我们需要做的，只是将上面的列表封装成一个 Python 迭代器；每一次迭代都返回一个稀疏向量即可。

```python
class MyCorpus(object):
    def __iter__(self):
        for line in open('mycorpus.txt'):
            # assume there's one document per line, tokens separated by whitespace
            yield dictionary.doc2bow(line.lower().split())
```

```python
corpus_memory_friendly = MyCorpus()  # doesn't load the corpus into memory!
for vector in corpus_memory_friendly:  # load one vector into memory at a time
    print(vector)
```

遍历语料库并打印每个文档向量，得到 corpus 中相同的结果，虽然输出与普通 Python 列表相同，但语料库现在对内存更友好，因为一次最多只有一个向量驻留在 RAM 中。

## 主题向量的变换
对文本向量的变换是 Gensim 的核心。通过挖掘语料中潜在的语义结构特征以及词之间的关系，最终可以变换出一个简洁高效的文本向量。  
  
在 Gensim 中，每一个向量变换的操作都对应着一个主题模型，doc2bow 变换就对应着词袋模型。下面以TF-IDF模型为例，介绍Gensim模型的一般使用方法。  
  
1. 模型对象的初始化。通常，Gensim 模型都接受一段训练语料（在 Gensim 中，语料对应着一个稀疏向量的迭代器）作为初始化的参数。显然，越复杂的模型需要配置的参数越多。  

```python
from gensim import models
tfidf = models.TfidfModel(corpus)
```
其中，corpus 是一个返回 bow 向量的迭代器。models.TfidfModel 对 corpus 中出现的每一个特征的 IDF 值的进行统计计算。  
  
2. 调用 tfidf 这个模型将语料（bow向量）转化成 TF-IDF 向量。  
注意：这里的 bow向量 必须与训练语料的 bow向量 共享同一个特征字典（即共享同一个向量空间，也就是corpus）。  
  
输出文档 TF-IDF 结果：
```python
corpus_tfidf = tfidf[corpus]
for doc in corpus_tfidf:
    print(doc)
```

3. 出于内存的考虑，model[corpus] 方法返回的是一个迭代器，若要多次访问 model[corpus] 的返回结果，可以先将其序列化到磁盘上。
```python
tfidf.save("./model.tfidf")
tfidf = models.TfidfModel.load("./model.tfidf")
```  
  
Gensim 内置多种主题模型的向量变换，包括 LDA，LSI，RP，HDP 等。这些模型通常以 bow 向量或 tfidf 向量的语料为输入，生成相应的主题向量。  
  
## LDA 实现 ——models.LdaModel
LDA API 详见：[models.LdaModel](https://radimrehurek.com/gensim/models/ldamodel.html)  
训练 LDA 模型：
```python
lda = models.LdaModel(corpus=None, num_topics=100, id2word=None, distributed=False, chunksize=2000, passes=1, update_every=1, alpha='symmetric', eta=None, decay=0.5, offset=1.0, eval_every=10, iterations=50, gamma_threshold=0.001, minimum_probability=0.01, random_state=None, ns_conf=None, minimum_phi_value=0.01, per_word_topics=False, callbacks=None, dtype=<type 'numpy.float32'>)
```

参数含义：
```python
corpus：bow 向量或 tfidf 向量的语料
num_topics：需要从训练语料库中提取的潜在主题的数量
id2word：word ids 到 words 的映射，即 dictionary，用于确定词汇大小、调试和主题打印
alpha 和 eta：影响文档-主题（theta）和主题-词（lambda）分布的稀疏性的超参数，默认值为symmetric：1.0/num_topics ；也可设置为 auto，用于自动学习对称先验
alpha：
eta：作为主题/词分布的对称先验的标量，可以将用户定义的非对称先验强加于词分布
minimum_probability：用于筛选主题
```

推断潜在主题：
```python
doc_topic = lda(corpus)
```

添加新文档到模型中：
```python
lda.update(other_corpus)
```

获取所有文档的主题分布：
```python
doc_topics = lda.get_document_topics(bow, minimum_probability=None, minimum_phi_value=None, per_word_topics=False)

bow: 语料向量
per_word_topics：true 的话对最可能的主题进行降序排序
```

打印主题：
```python
lda.print_topic(topic_id, topn=10)

Returns:    
String representation of topic, like ‘-0.340 * “category” + 0.298 * “$M$” + 0.183 * “algebra” + … ‘.
```

获取某 word 可能的主题：
```python
get_term_topics(word_id, minimum_probability=None)

Returns: 
The most likely topics for the given word. Each topic is represented as a tuple of (topic_id, term_probability).
```

获取某主题的 word：
```python
get_topic_terms(topicid, topn=10)

Returns:
(word_id, probability) 2-tuples for the most probable words in topic with id topicid.
```

## 文档相似性
在得到每篇文档对应的主题向量后，可以计算文档之间的相似度，进而完成如文本聚类、信息检索等任务。参考：[Similarity Queries](#https://radimrehurek.com/gensim/tut3.html)

