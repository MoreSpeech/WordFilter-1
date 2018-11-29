# WordFilter
A text filter completed in C++11 and implemented as a DFA algorithm. 以C++11完成的文字過濾器，並實作DFA算法。  

以C++11實作一文字過濾器，讀入過濾關鍵字表(key.txt)和要被過濾的文章(input.txt)，之後輸出過濾的結果  
專案所附的key.txt和input.txt皆包含英文繁中簡中跟日文的關鍵字，並基於UTF-8編碼所建立  

11/29更新AC自動機實作，時間複雜度為O(n)，實測結果僅需花0.000475秒，比先前O(nk)算法版本的0.001034秒更快  
針對Trie在記憶體上優化部分也提出Radix Tree的實作方式(更新於RadixTree分支)，理論上透過合併字串減少節點數方式，應能大幅降低記憶體占用，可惜實測結果並未能降低記憶體，Radix Tree版本僅做為參考用  

本程式實作兩種算法：暴力法(WordFilterNormal函式)，跟DFA算法(WordFilterDFA函式)，使用DFA算法前須先建立關鍵詞樹(CreateFilteredWordTree函式)  
為證實本程式在大量關鍵字下也能有不錯表現，程式會重複載入key.txt八次，達到223912個關鍵字數量  
經過實測，暴力法需花0.39738秒過濾測試樣本，DFA算法僅需花0.001034秒，DFA算法快了384倍！  
(PS.建立關鍵詞樹需花0.793057秒，但詞樹僅須建立一次)  

以上環境建置和測試皆使用ubuntu 16.04版  
測試環境為i7-6500U CPU @ 2.50GHz、7.8G記憶體、64位元  

PS.本程式未對UI做優化，也未實作回收記憶體  

=================================================================  
時間複雜度分析：(關鍵字數量m、被過濾文章長度n、最大關鍵字長度k)  
暴力法：O((n+k)m)  
DFA算法：O(nk)  

空間複雜度分析：(關鍵字數量m、被過濾文章長度n、最大關鍵字長度k)  
暴力法：O(n+km)  
DFA算法：O(n+km) (建立詞樹時，關鍵字都不重複或部分重疊的最差情況)  

在關鍵字數量極少而關鍵字長度均極長的情況下，DFA算法有可能輸給暴力法，其餘情況皆是DFA算法勝出  
關鍵字數量越大時兩者差異會更明顯  
