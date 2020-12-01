# Citeomatic

## Training
這邊依序是training的時候需要輸入的指令，皆來自[原作Github](https://github.com/allenai/citeomatic?fbclid=IwAR0lZIRnlw2ON9zNSqq7dBz4pE8VxeKDHAUC7mdRGYEn2YAfyRNx1ZFxwxM)。
**%run 開頭**直接打在jupyter notebook裡面讓他可以跑py檔。

注意：路徑、帳號名稱，需要適時更改。

### Hyperopt for Paper Embedder Model for DBLP
```
%run /mnt/sdb1/wwj0507/citeomatic/train.py --mode hyperopt --dataset_type dblp --n_eval 500 --model_name paper_embedder --models_dir_base /mnt/sdb1/wwj0507/citeomatic/data/hyperopts/dblp/ --version 5  &> /data/hyperopts/dblp/dblp.paper_embedder.hyperopt.log
```
### Paper Embedder Model for DBLP
先建立資料夾
```
mkdir data/comparison/dblp/models/trained/
```
去 ++/citeomatic/data/hyperopts/dblp/++ 找到相對應的資料夾(e.g.**citeomatic_hyperopt_paper_embedder_dblp_2019-12-26_5**)
```
%run /mnt/sdb1/wwj0507/citeomatic/train.py --mode train --dataset_type dblp --n_eval 500 --model_name paper_embedder --hyperopts_results_pkl /mnt/sdb1/wwj0507/citeomatic/data/hyperopts/dblp/citeomatic_hyperopt_paper_embedder_dblp_2019-12-26_5/hyperopt_results.pickle --models_dir_base /mnt/sdb1/wwj0507/citeomatic/data/comparison/dblp/models/trained/
```
#### Evaluating the Paper Embedder for DBLP 
```
%run ./evaluate.py --dataset_type dblp --candidate_selector_type ann --split test --paper_embedder_dir data/comparison/dblp/models/trained/paper_embedder/ --num_candidates 10 --ranker_type none
```
### Hyperopt for Citation Ranker Model
```
%run /mnt/sdb1/wwj0507/citeomatic/train.py --mode hyperopt --dataset_type dblp --models_ann_dir /mnt/sdb1/wwj0507/citeomatic/data/comparison/dblp/models/trained/paper_embedder/ --n_eval 500 --model_name citation_ranker --models_dir_base /mnt/sdb1/wwj0507/citeomatic/data/hyperopts/dblp/ --version 1 &> /mnt/sdb1/wwj0507/citeomatic/data/hyperopts/dblp/dblp.citation_ranker.hyperopt.log
```
### Citation Ranker Model for DBLP
去 ++/citeomatic/data/hyperopts/dblp/++ 找到相對應的資料夾(e.g.**citeomatic_hyperopt_citation_ranker_dblp_2019-12-29_1**)
```
%run /mnt/sdb1/wwj0507/citeomatic/train.py --mode train --dataset_type dblp --hyperopts_results_pkl /mnt/sdb1/wwj0507/citeomatic/data/hyperopts/dblp/citeomatic_hyperopt_citation_ranker_dblp_2019-12-29_1/hyperopt_results.pickle --n_eval 500 --model_name citation_ranker --models_ann_dir /mnt/sdb1/wwj0507/citeomatic/data/comparison/dblp/models/trained/paper_embedder/ --models_dir /mnt/sdb1/wwj0507/citeomatic/data/comparison/dblp/models/trained/citation_ranker/ --version 1 &> /mnt/sdb1/wwj0507/citeomatic/data/comparison/dblp/models/trained/dblp.citation_ranker.trained.log
```
![](https://i.imgur.com/7zV5gdo.png)

### evaluate: paper embedder
- 對**validation**的evaluate
```
%run /mnt/sdb1/wwj0507/citeomatic/evaluate.py --dataset_type dblp --candidate_selector_type ann --split valid --paper_embedder_dir /mnt/sdb1/wwj0507/citeomatic/data/comparison/dblp/models/paper_embedder/ --num_candidates 10 --ranker_type neural --citation_ranker_dir /mnt/sdb1/wwj0507/citeomatic/data/comparison/dblp/models/citation_ranker/
```

![](https://i.imgur.com/B5BvgVq.png)


- 對**test**的evaluate
```
%run /mnt/sdb1/wwj0507/citeomatic/evaluate.py --dataset_type dblp --candidate_selector_type ann --split test --paper_embedder_dir /mnt/sdb1/wwj0507/citeomatic/data/comparison/dblp/models/paper_embedder/ --num_candidates 10 --ranker_type neural --citation_ranker_dir /mnt/sdb1/wwj0507/citeomatic/data/comparison/dblp/models/citation_ranker/
```
![](https://i.imgur.com/s3Q1c8k.png)



---

### 其他部分
- assert False有可能會出錯，拿掉解決(原作者是說使用PyCharm會需要所以才加這行)
- 要寫`import tqdm.notebook as tqdm`才是對的，會跑出綠色進度條
## code
有更改過的code檔案：[drive](https://drive.google.com/drive/folders/1IspBNTvZFUQkViKAytTcRAP3cQW_HJxp?usp=sharing) 
而model資料夾裡面存放著目前我的model的參數

以下分別針對有更改過的code做簡單說明：

### build_db_test .py
- 在common.py裡面指定了各種檔案的位置：
![](https://i.imgur.com/H2CDhGF.png)
    - **json檔案存放位置：**/citeomatic/data/comparison/dblp/corpus.json
    - **db檔案存放位置：**/citeomatic/data/db/dblp.sqlite.db
- 前半段：把主要建立db的function拔出來獨立運作，從json建立db
![](https://i.imgur.com/6e55tXX.png)
- 後半段：找到有問題的兩筆資料(記得是錯在abstract/abstract raw裡面有數學式子，id分別為60751&60920)，後來有直接拿出來手動去掉奇怪的符號，建立了[json檔案](https://drive.google.com/file/d/13YXOk2DZrtSecT83PyHTuwtqZPkQ7P8h/view?usp=sharing) (應該是這個，如果錯了再改)，所以沒有用到後半段code(用來檢查並去掉詭異資料)就建立了[db檔案](https://drive.google.com/file/d/1MjvHxu9k1NfvAxjfFYoo09YU06f9omKJ/view?usp=sharing)(這個是確定可以跑的)
- 註：記得當時有遇到不明原因無法重新用同樣這個python檔案建立db的事故，但後來有重新建立成功，所以問題應該有順利排除

### corpus .py
- 建立db
- 在yield ProtoDoc的時候註解掉key_phrases的欄位
### train .py
- train_and_evaluate
    - 在train完model以後做validation
### training .py
- end_to_end_training
    - 記錄了所有training的步驟與順序
    - 讀進db的地方，命名為corpus
- 最後return的地方加入map
    ![](https://i.imgur.com/4gHi2aB.png)

### neighbors .py
- 在跑Citation Ranker Model for DBLP的時候會遇到找不到id=27902的錯誤，試過無法直接排除，於是更改成以下寫法，用try&except可解決此問題
    ![](https://i.imgur.com/0lcAqHm.png)

### eval_metrics .py
- 在**precision_recall_f1_at_ks** function裡面建立了新的metrics: **_map**
    ![](https://i.imgur.com/9PN69me.png)
    其餘後續部分也建立了針對map值儲存的地方。


