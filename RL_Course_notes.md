# RL

## b的用意

<img src="C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201028102408103.png" alt="image-20201028102408103" style="zoom: 50%;" />

若沒有sample到的action會減少被sample到的機率，

## Q-learning

- value-based: learn critic: 不是直接採取行為，而是評價目前行為的好壞
- state value function V^pi(s): 預期我得到的reward多少
- state/actor 兩者都會影響V^pi(s)
- 估測V(s)的方法：
  - mc based apporach: 要把遊戲玩完才可估測，某個state出現的 cumulated reward
  - td apporach: 可知兩次差了r_t ![image-20201028103019923](C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201028103019923.png)
  - 兩者比較：(td比較常見)
    - mc has larger variance: 因為遊戲本身有隨機性，且是看大R(G_a)
    - td 僅有小r有隨機性，但variance會比Ga小，但可能下一個V(s_t+1)會估不準
    - 舉例：
    - <img src="C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201028103339226.png" alt="image-20201028103339226" style="zoom:50%;" />

- 另一種critic方式：Q^pi(s,a)
  - <img src="C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201028103620577.png" alt="image-20201028103620577" style="zoom:50%;" />
  - 看state, action，每次找到一個新的pi，找到一個更好的pi
  - 在state s 裡面不一定會採取action a，Q function的定義是`actor pi 若一直強制採取action a，用pi一直互動下去，得到的expected reward`
  - tune 好 Q 就是找到pi'
  - <img src="C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201028104159926.png" alt="image-20201028104159926" style="zoom:50%;" />
  - (證明)為甚麼找出來的`V^pi'(s)>=V^pi(s)`
  - **[TIPS1] target network** 
    - 在learn Q function的時候會用到TD的概念
    - 希望差了一個r_t，但純粹model成regression的問題不太好解，因為同一個input，其target是會一直變動的
    - 通常會先把下面的Q fixed，也就是target network，因此r_t是fixed value，tuningQ^pi學習r_t就是一種regression的問題
    - <img src="C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201028104901824.png" alt="image-20201028104901824" style="zoom:67%;" />
    - (問題)因為input不一樣：一個是s_t一個是s_t+1，所以r_t不會是0
  - **[TIPS2] exploration**
    - 如果有三種action，其中一個被採取過且reward為正，actor就會一直sample那個action，其他action就完全不會被選到 -> 不知道其他action是否會比較好？ 
    - 兩個方法解決此問題：
      - epsilon greedy: epsilon would decay
      - boltzmann exploration
      - <img src="C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201028105434330.png" alt="image-20201028105434330" style="zoom:50%;" />
  - **[TIPS3] Replay Buffer**
    - replay buffer裡面的紀錄(exp)有可能來自不同的policy
    - 只有在裝滿的時候才會把舊的丟掉
    - off-policy的作法
    - <img src="C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201028111925271.png" alt="image-20201028111925271" style="zoom:50%;" />

## References

https://www.youtube.com/watch?v=W8XF3ME8G2I

https://www.youtube.com/watch?v=o_g9JUMw1Oc

