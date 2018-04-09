# Gensim

Gensim 是一个开源的 Python 库，用于从原始的非结构化的文本中，无监督地学习到文本潜在的主题向量表达。除了具备基本的预料处理功能外，Gensim 还支持包括 TF-IDF，LSA，LDA，和 word2vec 在内的多种主题模型算法，支持流式训练（online training），并提供了诸如相似度计算，信息检索等一些常用任务的 API 接口。  

## 基本概念
### Corpus
Corpus(语料) 也称为训练语料库，是一组原始文本的集合，是 Gensim 的输入，用于无监督的训练文本主题的潜在结构。从语料中推断出的潜在结构，可以用来对一个新的文档指定一个主题。训练过程不需要人工干预，主题分类是无监督的。

### Vector
在 VSM (Vector Space Model) 中，每个文档都由一组特征表示。

### Sparse Vector
稀疏向量：我们可以略去向量中多余的0元素。此时，向量中的每一个元素是一个 (key, value) 的 tuple。

### Model
在向量化了语料之后，可以使用各种模型。模型 Model 指的是一个文档表示到另一个文档表示的转换。在 Gensim 中，文档用向量来表示，所以模型可以认为是在两个向量空间进行转换。这个转换是从训练语料库中学习出来的。

## 训练预料的预处理
训练语料的预处理指的是将文档中原始的字符文本转换成Gensim模型所能理解的稀疏向量的过程。  

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
>>> class MyCorpus(object):
>>>     def __iter__(self):
>>>         for line in open('mycorpus.txt'):
>>>             # assume there's one document per line, tokens separated by whitespace
>>>             yield dictionary.doc2bow(line.lower().split())
```

```python
>>> corpus_memory_friendly = MyCorpus()  # doesn't load the corpus into memory!
>>> for vector in corpus_memory_friendly:  # load one vector into memory at a time
>>> print(vector)
```

遍历语料库并打印每个文档向量，得到 corpus 中相同的结果，虽然输出与普通 Python 列表相同，但语料库现在对内存更友好，因为一次最多只有一个向量驻留在 RAM 中。

### 主题向量的变换
