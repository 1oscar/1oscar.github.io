---
layout: post
title: "一则实例讲述tensorflow深度学习模型DNN的使用"
comments: true
share: true
tags: tensorflow,机器学习
---

执行环境：

ubuntu： 16.04
tensorflow： 1.4.1
cudn: 8.0,cudnn: 6.0
python: 2.7.12

从总体上看，实例可以分成两个部分： 构建深度学习模型和执行模型部分。

代码中训练集120*4,测试集30*4。

下面代码中解释

```

from __future__ import absolute_import
from __future__ import division
from __future__ import print_function

#__future__ 引入python3中的一些特性，导入这个包便可以用python3中的
#一些特性来代替python2中的，比如print在python3中是函数，实际使用就要print()


import numpy as np
from sklearn import datasets
from sklearn import metrics
from sklearn import model_selection
import tensorflow as tf


X_FEATURE = 'x'  # Name of the input feature.
#这个是必须这样命名，后面会用到。

def main(unused_argv):
  # Load dataset.
  iris = datasets.load_iris()
  #sklearn默认数据集
  x_train, x_test, y_train, y_test = model_selection.train_test_split(
      iris.data, iris.target, test_size=0.2, random_state=42)
  #sklearn中的分割训练和测试数据集的 test_size是测试集合占总集合的比例。
  #总的150*0.2=30是测试集合。random_state表示：产生的结果是固定的，意思就是每次的测试集合分割出来都是这些数字。
  #random_stage一般是和shuffle一起使用，当shuffle默认是True时，和这个一起使用表示表示可放回抽样，
  #每次都是一样的结果。train_test_split默认shuffle是True。

  # You can define you configurations by providing a RunConfig object to
  # estimator to control session configurations, e.g. tf_random_seed.
  run_config = tf.estimator.RunConfig().replace(tf_random_seed=1)
  #tf_random_seed 要替换的参数。代码里有参数校验，替换的参数必须是源码里指定的。这里可是设置模型的路径，
  #model_dir设置模型的路径。
  #官方解释： Random seed for TensorFlow initializers. Setting this value allows consistency between reruns.
  
  '''
  不是很理解它存在的作用。
  '''

  # Build 3 layer DNN with 10, 20, 10 units respectively.
  feature_columns = [
      tf.feature_column.numeric_column(
              X_FEATURE, shape=np.array(x_train).shape[1:])]
  '''
  numeric_column取的是特征列，示例，： 
   price = numeric_column('price')
  columns = [price, ...]
  因为下面numpy_input_fn有参数key=x，所以这里设置成X_FEATURE为x，存在的意义就是和源码里的保持一致。
  '''
  classifier = tf.estimator.DNNClassifier(
      feature_columns=feature_columns, hidden_units=[10, 20, 10], n_classes=3,
      config=run_config)
  '''
  使用DNN深度学习分类模型，这里是多分类，最终分成了多个类。
  hidden_units表示使用3层神经网络，每一层的节点数分别是10,20，,10，表示可每层迭代此时是10，,20,30.
  
  '''
  

  # Train.
  train_input_fn = tf.estimator.inputs.numpy_input_fn(
      x={X_FEATURE: x_train}, y=y_train, num_epochs=None, shuffle=True)
  '''
  构建模型前的参数设置。
  
  x=表示指定特征数据列。y=表示要分的那几类。
  num_epochs官方解释；Integer, number of epochs to iterate over data. If `None` will
      run forever.表示在所有数据上迭代次数，这里表示不迭代。
  补充：
  bachsize：表示每次训练样本的样本数。
  epoch表示：对所有样本训练的次数。
  iteration： 使用bachsize训练一次表示一次iteration。
  shuffle表示可放回抽样。
  
  '''
  classifier.train(input_fn=train_input_fn, steps=200)
  
  '''
  train训练模型。input_fn训练模型的一些配置，包括参数，模型路径，训练样本，多线程，可放回，轮训次数等。
  steps官方解释：
  Number of steps for which to train model. If `None`, train forever
        or train until input_fn generates the `OutOfRange` error or
        `StopIteration` exception. 'steps' works incrementally. If you call two
        times train(steps=10) then training occurs in total 20 steps. If
        `OutOfRange` or `StopIteration` occurs in the middle, training stops
        before 20 steps. If you don't want to have incremental behavior please
        set `max_steps` instead. If set, `max_steps` must be `None`.
        
   此参数设置了，max_steps就不用设置了。
   意思是：训练模型的步长。如果为none，就永远都在训练，直到输入数据迭代时候产生越界才停止。
   如果你步长20，调用两次，则训练时候总共是20步长。如果中间越界了，会选在20步长之前停止。
  
  '''

  # Predict.
  test_input_fn = tf.estimator.inputs.numpy_input_fn(
      x={X_FEATURE: x_test}, y=y_test, num_epochs=1, shuffle=False)
  '''
  执行模型前的参数设置。
  
  
  '''
  predictions = classifier.predict(input_fn=test_input_fn)
  '''
  预测
  '''
  y_predicted = np.array(list(p['class_ids'] for p in predictions))
  
  '''
  列表推导式。
  得到预测的分类结果。class_ids是固定的key值，在源码里设置。
  这里是分类，每个p的结果是：
  {'probabilities': array([1.5384521e-05, 2.0704072e-02, 9.7928053e-01], dtype=float32), 'logits': array([-9.901466 , -2.6967423,  1.1597455], dtype=float32), 'classes': array(['2'], dtype=object), 'class_ids': array([2])}
  如果是回归，参数会有变化。
  因为测试集是30*4，所以这里会有30个calss_ids。
  
  '''
  y_predicted = y_predicted.reshape(np.array(y_test).shape)
  #把预测的值转换为y_test的行与列。

  # Score with sklearn.
  score = metrics.accuracy_score(y_test, y_predicted)
  print('Accuracy (sklearn): {0:f}'.format(score))
  metrics模块其他评价分类效果的指标还有以下函数：
  f1_score(),
  precision_recall_fscore_support： 精确率，召回率，fscore值。
  precision_score：精确率
  recall_score
  hamming_loss（）
  log_loss（）
  hinge_loss（）
  brier_score_loss（）
  zero_one_loss（）
  jaccard_similarity_score（）jaccard相似性计算等等
  
  '''
  sklearn里的metrics里的函数计算准确度。
  此外，
  
  '''

  # Score with tensorflow.
  scores = classifier.evaluate(input_fn=test_input_fn)
  print('Accuracy (tensorflow): {0:f}'.format(scores['accuracy']))
  
  '''
  tf的evaluate函数：同sklearn的metrics，实现模型一些效果的计算与衡量。
  scores结果：
  {'average_loss': 0.09192087, 'accuracy': 0.96666664, 'global_step': 200, 'loss': 2.757626}
  
  '''


if __name__ == '__main__':
  tf.app.run()
  
'''
执行本代码，代码默认是从main()函数开始执行的。
别人调用本代码，直接调用模块名即可。


'''


```



