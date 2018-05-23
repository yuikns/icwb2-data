# icwb2-data

**Source**:

+ [homepage](http://sighan.cs.uchicago.edu/bakeoff2005/)
+ [introduction by 52nlp](http://www.52nlp.cn/%E4%B8%AD%E6%96%87%E5%88%86%E8%AF%8D%E5%85%A5%E9%97%A8%E4%B9%8B%E8%B5%84%E6%BA%90)


SIGHAN是国际计算语言学会（ACL）中文语言处理小组的简称，其英文全称为“Special Interest Group for Chinese Language Processing of the Association for Computational Linguistics”，又可以理解为“SIG汉“或“SIG漢“。而Bakeoff则是SIGHAN所主办的国际中文语言处理竞赛，第一届于2003年在日本札幌举行（Bakeoff 2003),第二届于2005年在韩国济州岛举行(Bakeoff 2005), 而2006年在悉尼举行的第三届（Bakeoff 2006）则在前两届的基础上加入了中文命名实体识别评测。目前SIGHAN Bakeoff已成功举办了6届，其中Bakeoff 2005的数据和结果在其主页上是完全免费和公开的，但是请注意使用的前提是非商业使用（non-commercial）:


> The data and results for the 2nd International Chinese Word Segmentation Bakeoff are now available for non-commercial use.

在Bakeoff 2005的主页上，我们可以找到如下一行：“The complete training, testing, and gold-standard data sets, as well as the scoring script, are available for research use”，在这一行下面提供了三个版本的icwb2-data。下载解压后，通过README就可以很清楚的了解到它包含哪些中文分词资源，特别需要说明的是这些中文分词语料库分别由台湾中央研究院（Academia Sinica）、香港城市大学（City University of Hong Kong）、北京大学(Peking University)及微软亚洲研究院（Microsoft Research）提供，其中前二者是繁体中文，后二者是简体中文,以下按照README简要介绍icwb2-data:

### 1) 介绍（Introduction）

本目录包含了训练集、测试集及测试集的（黄金）标准切分，同时也包括了一个用于评分的脚本和一个可以作为基线测试的简单中文分词器。(This directory contains the training, test, and gold-standard data used in the 2nd International Chinese Word Segmentation Bakeoff. Also included is the script used to score the results submitted by the bakeoff participants and the simple segmenter used to generate the baseline and topline data.)

### 2) 文件列表（File List）

在gold目录里包含了测试集标准切分及从训练集中抽取的词表（Contains the gold standard segmentation of the test data along with the training data word lists.）

+ 在scripts目录里包含了评分脚本和简单中文分词器（Contains the scoring script and simple segmenter.）
+ 在testing目录里包含了未切分的测试数据（Contains the unsegmented test data.）
+ 在training目录里包含了已经切分好的标准训练数据（Contains the segmented training data.）
+ 在doc目录里包括了bakeoff的一些指南（Contains the instructions used in the bakeoff.）

### 3) 编码（Encoding Issues）

文件包括扩展名”.utf8”则其编码为UTF-8(Files with the extension “.utf8″ are encoded in UTF-8 Unicode.)

文件包括扩展名”.txt”则其编码分别为（Files with the extension “.txt” are encoded as follows）:

+ 前缀为 `as\_`，代表的是台湾中央研究院提供，编码为Big Five (CP950)；
+ 前缀为 `hk\_`，代表的是香港城市大学提供，编码为Big Five/HKSCS；
+ 前缀为 `msr\_`，代表的是微软亚洲研究院提供，编码为 EUC-CN (CP936)；
+ 前缀为 `pku\_`，代表的北京大学提供，编码为EUC-CN (CP936)；

EUC-CN即是GB2312（EUC-CN is often called “GB” or “GB2312″ encoding, though technically GB2312 is a character set, not a character encoding.）

### 4） 评分（Scoring）

评分脚本“score”是用来比较两个分词文件的，需要三个参数（The script ‘score’ is used to generate compare two segmentations. The script takes three arguments)：

1. 训练集词表（The training set word list）
2. “黄金”标准分词文件（The gold standard segmentation）
3. 测试集的切分文件（The segmented test file）
　

以下利用其自带的中文分词工具进行说明。在scripts目录里包含一个基于最大匹配法的中文分词器mwseg.pl，以北京大学提供的人民日报语料库为例，用法如下：

```
./mwseg.pl ../gold/pku_training_words.txt < ../testing/pku_test.txt > pku_test_seg.txt
```

其中第一个参数需提供一个词表文件pku_training_word.txt，输入为pku\_test.txt，输出为pku\_test\_seg.txt。

利用score评分的命令如下：

```
./score ../gold/pku_training_words.txt ../gold/pku_test_gold.txt pku_test_seg.txt > score.txt
```

其中前三个参数已介绍，而score.txt则包含了详细的评分结果，不仅有总的评分结果，还包括每一句的对比结果。这里只看最后的总评结果：

```
= SUMMARY:
=== TOTAL INSERTIONS:	9274
=== TOTAL DELETIONS:	1365
=== TOTAL SUBSTITUTIONS:	8377
=== TOTAL NCHANGE:	19016
=== TOTAL TRUE WORD COUNT:	104372
=== TOTAL TEST WORD COUNT:	112281
=== TOTAL TRUE WORDS RECALL:	0.907
=== TOTAL TEST WORDS PRECISION:	0.843
=== F MEASURE:	0.874
=== OOV Rate:	0.058
=== OOV Recall Rate:	0.069
=== IV Recall Rate:	0.958
###	pku_test_seg.txt	9274	1365	8377	19016	104372	112281	0.907	0.843 0.874	0.058	0.069	0.958
```

说明这个中文分词器在北大提供的语料库上的测试结果是：召回率为90.7%，准确率为84.3%，F值为87.4%等。

SIGHAN Bakeoff公开资源的一个重要意义在于这里提供了一个完全公平的平台，任何人都可以拿自己研究的中文分词工具进行测评，并且可以和其公布的比赛结果对比，是驴子是马也就一目了然了。



***以下是说明原文***


> 2nd International Chinese Word Segmentation Bakeoff - Data Release
> Release 1, 2005-11-18

## Introduction

This directory contains the training, test, and gold-standard data used in the 2nd International Chinese Word Segmentation Bakeoff. Also included is the script used to score the results submitted by the bakeoff participants and the simple segmenter used to generate the baseline and topline data.

## File List

```
gold/       Contains the gold standard segmentation of the test data
            along with the training data word lists.

scripts/    Contains the scoring script and simple segmenter.

testing/    Contains the unsegmented test data.

training/   Contains the segmented training data.

doc/        Contains the instructions used in the bakeoff.
```

## Encoding Issues

Files with the extension ".utf8" are encoded in UTF-8 Unicode.

Files with the extension ".txt" are encoded as follows:

+ as_    Big Five (CP950)
+ hk_    Big Five/HKSCS
+ msr_   EUC-CN (CP936)
+ pku_   EUC-CN (CP936)

EUC-CN is often called "GB" or "GB2312" encoding, though technically GB2312 is a character set, not a character encoding.

## Scoring

The script 'score' is used to generate compare two segmentations. The script takes three arguments:

1. The training set word list
2. The gold standard segmentation
3. The segmented test file

You must not mix character encodings when invoking the scoring
script. For example:

```
% perl scripts/score gold/cityu_training_words.utf8 gold/cityu_test_gold.utf8 test_segmentation.utf8 > score.ut8
```

## Licensing

The corpora have been made available by the providers for the purposes of this competition only. By downloading the training and testing corpora, you agree that you will not use these corpora for any other purpose than as material for this competition. Petitions to use the data for any other purpose MUST be directed to the original providers of the data. Neither SIGHAN nor the ACL will assume any liability for a participant's misuse of the data.

## Question?

Questions or comments about these data can be sent to Tom Emerson, tree@sighan.org.

