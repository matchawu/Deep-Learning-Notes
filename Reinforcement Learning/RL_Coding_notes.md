# RL Coding notes

## Customized Environment

>  以openAI gym為基底做出DQN的自定義環境

主要透過這個回答裡面的步驟實現：[ref link](https://stackoverflow.com/questions/44469266/how-to-implement-custom-environment-in-keras-rl-openai-gym) [code link](https://github.com/openai/gym/blob/master/gym/envs/toy_text/hotter_colder.py) [ref link 2](https://stackoverflow.com/questions/45068568/how-to-create-a-new-gym-environment-in-openai)

code link 裡面的 GitHub code 說明很詳盡

1. Constructor__init__ method
2. Action space
3. Observation space (see https://github.com/openai/gym/tree/master/gym/spaces for all available gym spaces (it's a kind of data structure))
4. _seed method (not sure that it's mandatory)
5. _step method accepting action as a param and returning observation (state after action), reward (for transition to new observational state), done (boolean flag), and some optional additional info.
6. _reset method that implements logic of fresh start of episode.

### 檔案架構

除了define myEnv以外，import自身的environment的時候需要按照一定的檔案架構，參考ref link 2。

[我自建的架構](https://github.com/matchawu/gym-graph) 是按照ref link 2寫成的。接著在code中引入：

```python
import gym
import gym_graph
env = gym.make('gym_graph:graph-v0')
```

目前尚未釐清：

​	是要直接`pip install`還是`pip install -e .`？兩者的差異為何？

### 需要注意的部分

action_space & observation_space

可以參考 [官方文檔](https://gym.openai.com/docs/#spaces)

```python
self.action_space = spaces.Box(low=np.array([-self.bounds]), high=np.array([self.bounds]),dtype=np.float32)

self.observation_space = spaces.Discrete(4)
```

done

```python
done = self.guess_count >= self.guess_max
```

### 問題

在做完上述步驟以後，一直卡在以下的問題：

```python
import gym
import gym_graph
env = gym.make('gym_graph:graph-v0')
```

第二行會出現以下錯誤：

```
---------------------------------------------------------------------------
ModuleNotFoundError                       Traceback (most recent call last)
<ipython-input-11-e98577d7cfae> in <module>
      1 import gym
----> 2 import gym_graph
      3 env = gym.make('gym_graph:graph-v0')

ModuleNotFoundError: No module named 'gym_graph'
```

後來的解法：

> 不需要引入至gym底下，直接當成一個function即可