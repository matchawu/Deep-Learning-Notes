# Q Learning

![img](https://cdn-media-1.freecodecamp.org/images/1*jmcVWHHbzCxDc-irBy9JTw.png)

```markdown
New Q value =    Current Q value +    lr * [Reward + discount_rate * (highest Q value between possible actions from the new state s’ ) — Current Q value ]
```



![img](https://pic4.zhimg.com/80/v2-da914a9774f409116731f3a2492be9f3_720w.jpg)

link:https://zhuanlan.zhihu.com/p/35882937



讓人看得懂的講義：http://debussy.im.nuu.edu.tw/sjchen/MachineLearning/final/DeepRL.pdf

![image-20201111172945202](C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201111172945202.png)



agent會先踩過一些(s,a,r,s')，存入memory，待蒐集超過(batch size)以後，開始train Q。

replay buffer & train Q: random sample batch size大小的存在memory裡面的(s,a,r,s')

兩個一起更新的話，target會一直變動(不好train)，因此先fix住右邊的，讓左邊學習就變成了regression的版本，再把左邊學好的參數給右邊。









---

### References

https://blog.csdn.net/itplus/article/details/9361915

https://www.freecodecamp.org/news/diving-deeper-into-reinforcement-learning-with-q-learning-c18d0db58efe/

http://baijiahao.baidu.com/s?id=1597978859962737001&wfr=spider&for=pc