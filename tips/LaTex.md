# LaTeX

## 表格中自動換行

有鑑於朋友向我提出了這個問題，不然她的表格只能90度旋轉地放。

在查了許多資料以後，覺得以下的方法最直觀、最容易讓人理解及應用。

以下步驟：

1. 先設定一個新的命令，叫作 `\tabincell`

   ```python
   \newcommand{\tabincell}[2]{\begin{tabular}{@{}#1@{}}#2\end{tabular}}
   ```

2. 接著，再用以下的方式呈現表格

   ```python
   \begin{table}
   	\begin{tabular}{|c|c|}
           \hline
           1 & the first line \\
           \hline
           2 & \tabincell{c}{haha\\ heihei\\zeze} \\
           \hline
   	\end{tabular}
   \end{table}
   ```

如果直接用source上面的LaTeX去貼上，會發現錯誤，因為斜線反方向了!!!

因此記得貼上面的(我已改過)，並記得在tabular外面再包一層table。



source: https://blog.csdn.net/virhuiai/article/details/7886265