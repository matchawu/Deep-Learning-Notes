# Tensorflow

### Session

```python
sess = tf.Session()
sess.tf.global_variables_initializers()
# saver = tf.train.Saver() ### 還沒有確認意思
sess.run(something)
```

目前使用DDQN + GVAT，因為GVAT中間需要重train，所以把session分開來寫，一個sess for DQN，一個sess_graph for GVAT。

### variable_scope

在需要的變數前面加上名字，有點像是樹狀結構的方式去命名。

參考莫凡的寫法：

```python
sess = tf.Session()
with tf.variable_scope('Natural_DQN'):
    natural_DQN = DoubleDQN(
        n_actions=ACTION_SPACE, n_features=OBSERVATION_SPACE, memory_size=MEMORY_SIZE,
        e_greedy_increment=0.001, double_q=False, sess=sess
    )

with tf.variable_scope('Double_DQN'):
    double_DQN = DoubleDQN(
        n_actions=ACTION_SPACE, n_features=OBSERVATION_SPACE, memory_size=MEMORY_SIZE,
        e_greedy_increment=0.001, double_q=True, sess=sess, output_graph=True)

sess.run(tf.global_variables_initializer()) # DQN的variables只需要initialize這一次
```

何教授的寫法：

```python
with tf.variable_scope("VGCN") as scope:
    ......
```

可以印出來變數的名稱前面都會有scope上面命名的東西。

### trainable_variables

```python
for var in tf.trainable_variables(scope='VGCN'): # 可以指定要哪個scope底下的變數，或是不指定就印出全部
    print(var) # 印出資訊
    print(self.sess_graph.run(var)) # 印出值
```

### 初始化

透過印出variable的方式去確定是否每次initialize GVAT 還沒開始train的時候 網路是有一樣的參數的

https://ithelp.ithome.com.tw/articles/10187786

### training時間越來越長

在train我的鬼怪GCNDQN的時候，發現到超過300episode的時候速度整個超慢，因此腦袋裡突然浮現了重複使用variable而variable scope後面多了`"_1","_2","_3"`的印象......看起來是長起來了。

之前產學用的方法就是del掉所有不要的變數，這邊也是用這樣的方法。[可以參考](https://stackoverflow.com/questions/58435961/tensorflow-delete-graph-and-free-up-resources)

```python
del self.sess_graph, self.saver
```

我在每次train完GCN的時候把session跟saver拿掉，發現這樣印出來確認以後，我的variable後面就不會有之一之二之三了。

印出來的方法：

```python
for var in tf.trainable_variables():
    print(var) # 印出名稱
    print(sess.run(var)) # 印出值
```

這部分其實還沒有到很會用，有機會再多寫一些。

### 只初始化部分參數

因為`tf.global_variables_initializers()`會初始化所有他看得到的參數。因為這邊我只需要重新初始化GCN的參數而不需要重新初始化DDQN，所以用了[這個網站](https://stackoverflow.com/questions/46823476/tensorflow-how-to-initlialize-all-variables-in-a-given-variable-scope)找到的方法：

```python
my_scope = 'my_scope_name'
scope_variables=  tf.get_collection(tf.GraphKeys.VARIABLES, scope=my_scope)

# 這裡可以print(sess.run(scope_variables)去確認是不是要init的那些參數

init_scope = tf.variables_initializer(scope_variables, name="init_"+my_scope )
sess.run(init_scope)
```

