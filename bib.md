# Convert .bib to .bbl

## 基本操作

https://blog.csdn.net/JSJWR/article/details/79373900?fbclid=IwAR2jEqa8_S7CHl_rWJuCPFTBy0X-wxUtEX1N6hyXv3jOfNbnLhXFYo_YE8E

按照步驟做，才可以得到IEEE要的bbl格式的檔案，再把檔案內容貼到.tex檔裡面。



### 會遇到的問題

系統找不到指定檔案等路徑問題：

https://www.cnblogs.com/lmj-sky/p/7153918.html

裡面主要提到了MikTeX這個東西，可以看到其實在開啟TeXStudio時也會說明是否有這個東西，如果沒有的話是沒辦法執行的。因此先去安裝MikTeX：https://miktex.org/download。

此時要記得MikTeX安裝的點在哪，或是在安裝完成以後再去開始工作列上面右鍵開啟檔案位置。

回到WinEdt，點Options> Execution Modes

<img src="C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201130235034158.png" alt="image-20201130235034158" style="zoom:80%;" />

裡面的TeX System包含了執行所需要的路徑。

<img src="C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201130235125491.png" alt="image-20201130235125491" style="zoom:80%;" />

從前面可以看到，我原本auto指向的資料夾裡面是沒有東西的(因為我根本還沒安裝MikTeX)。因此在安裝以後，依序找到miktex資料夾、bin資料夾、doc資料夾，以及yap.exe檔案的位置，按下Apply和OK。重新編譯所需要的檔案就可以成功。

## 註

1. 建立一個main.tex，裡面貼上

   ```
   \documentclass[preprint,review,12pt,authoryear]{elsarticle}
   \begin{document}
   \nocite{*}
   \bibliographystyle{plain}
   \bibliography{ref}
   \end{document} 
   ```

   裡面的{ref}代表你的.bib檔案的檔名(不需要.bib)

2. 也在WinEdt視窗開啟ref.bib，也就是你的bib檔案

3. 按下 PDFLaTeX，再按下 TeX>BibTeX 就可以在這個資料夾底下產生對應的.bbl檔案。複製.bbl檔案的內容倒IEEE的.tex即可。

   ![image-20201130235604641](C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201130235604641.png)

![image-20201130235703208](C:\Users\wwj\AppData\Roaming\Typora\typora-user-images\image-20201130235703208.png)