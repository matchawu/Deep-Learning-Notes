# RL Coding notes

## Customized Environment

>  以openAI gym為基底做出DQN的自定義環境

主要透過這個回答裡面的步驟實現：[ref link](https://stackoverflow.com/questions/44469266/how-to-implement-custom-environment-in-keras-rl-openai-gym) [code link](https://github.com/openai/gym/blob/master/gym/envs/toy_text/hotter_colder.py) 

code link 裡面的 GitHub code 說明很詳盡

1. Constructor__init__ method
2. Action space
3. Observation space (see https://github.com/openai/gym/tree/master/gym/spaces for all available gym spaces (it's a kind of data structure))
4. _seed method (not sure that it's mandatory)
5. _step method accepting action as a param and returning observation (state after action), reward (for transition to new observational state), done (boolean flag), and some optional additional info.
6. _reset method that implements logic of fresh start of episode.

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



---



