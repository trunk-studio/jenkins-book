敏捷開發方法
==========

什麼是敏捷？先從豐田式生產（精實生產）開始談起！

豐田式生產
---------

如果想瞭解持續整合的目的，就需要先知道豐田式生產管理（Toyota Management）的概念，豐田式生產又稱為精實生產（Lean Producton）或簡稱 TPS（Toyota Production System）。

維基百科對[豐田生產方式][1]的定義：

> 豐田式生產主要目標，是杜絕負荷過重（muri）、不平準（mura）和一切的浪費（muda）。TPS 把浪費歸納成七種：
>
> 1.	等待的浪費；
> 2.	搬運的浪費；
> 3.	不良品的浪費；
> 4.	動作的浪費；
> 5.	加工的浪費；
> 6.	庫存的浪費；
> 7.	製造過多（早）的浪費。

TPS 背後的理念就是「杜絕浪費」，包括在製造業難以避免的庫存堆積。基本原則是「豐田模式」（The Toyota Way），概述如下：

1.	正確的流程方能產生正確結果
2.	發展員工與事業夥伴，以為組織創造價值
3.	持續解決根本問題是組織型學習的驅動力

從製造業的角度來看，只要能避免不必要的浪費與重工，相對來說，效率就會變得更快更好；我們把 TPS 歸納的七種浪費，改從軟體開發的角度來看：

1.	**等待的浪費，搬運的浪費：**<br/>程式開發週期除寫程式外，建構（build）、測試（test）與部署（deploy）都是必要的流程，需要透過自動化建置來杜絕各環節的浪費。
2.	**不良品的浪費：**<br/>可以預期的是，程式錯誤（bug）只會一再地發生，不可能完全避免；但是若能夠在每個環節多進行測試與確認，則可以確保每個小動作能被正常執行，特別是在每次程式的修改後，應立即進行完整的測試，盡可能減少錯誤的產生。
3.	**動作的浪費，加工的浪費：**<br/>不斷被重覆的動作，就是一種浪費；每個人的時間和精力有限，能夠透過程式來取代人力介入的流程，就應該及早被自動化。
4.	**庫存的浪費：**<br/>很幸運地，軟體通常沒有庫存壓力；但是隨著程式碼增長，無法被測試的程式碼一旦堆積過多，就會帶來可怕的除錯夢靨。
5.	**製造過多（早）的浪費：**<br/>非必要或事先考慮過多的功能需求，除開發過程已浪費不少時間，寫出來的程式也增加維護成本。

所有在製造業所會發生的問題，大部份軟體開發也會有同樣的問題，我們可以借鏡其精神，與豐田式生產相互輝映，發展出敏捷式開發（Agile Development）。

敏捷式開發
=========

**持續整合**是「敏捷軟體開發」重要的一個環節，就跟豐田式生產一樣，敏捷軟體開發也致力於杜絕所有可能的浪費。

維基百科對[敏捷軟體開發][2]的定義：

> 敏捷軟體開發（英語：Agile Software Development），又稱敏捷開發，是一種從 1990 年代開始逐漸引起廣泛關注的一些新型軟體開發方法，是一種應對快速變化的需求的一種軟體開發能力。它們的具體名稱、理念、過程、術語都不盡相同，相對於「非敏捷」，更強調程式設計師團隊與業務專家之間的緊密協作、面對面的溝通（認為比書面的文檔更有效）、頻繁交付新的軟體版本、緊湊而自我組織型的團隊、能夠很好地適應需求變化的代碼編寫和團隊組織方法，也更注重軟體開發中人的作用。

敏捷開發宣言
-----------

- 個人與互動**重於**流程與工具：避免資訊的錯誤，浪費溝通的時間。
- 可用的軟體**重於**詳盡的文件：若詳盡的文件就是可用的軟體，可避免維護兩個地方，且文件就是運作結果本身。
- 與客戶合作**重於**合約協商：客戶才是需求的本身，與客戶合作將更接近目標，不會花錯力氣。
- 回應變化**重於**遵循計劃：唯一不變的就是變，計畫趕不上變化，如果只是不知變通的依計劃進行，往往知道方向錯了已來不及。

持續整合與改善
------------

持續整合的先行條件，就是專案必須規劃良好的測試機制，將規格（Spec）清楚定義成為可被自動執行的測試流程。

有清楚的規格可以用來檢驗系統的功能，在上線後每次*異常狀況*發生時，就能將遇到的問題，制定成新加入的規格，用更多的測試代碼來確保系統品質，讓**除錯**的成果能被累積、保存在規格之中，如此一來就能累積成為系統品質的後盾。

搭配可以自動化執行的測試規格，就能利用 Jenkins 定時產生測試報告，讓專案相關人員隨時注意專案的健康指數，及早發現問題並儘早治療。

進行自動化建置與測試的時間點，可能發生在每個 Code Commit 之後，也可能由人為控制觸發；無論如何，要搭配 Jenkins 做到持續整合，建議至少要進行每日及每週的建置任務。

### Daily Build

Or Nightly Build...

1.	每天早晚或中午，進行一次完整性的建置。
2.	建置前需要通過所有的測試。
3.	發生錯誤時，需要當日確認，並修正完畢。
4.	建置完成後，部署到 QA 機器進行測試。

### Weekly Build

1.	每週進行一次完整性的建置。
2.	建置前需要通過所有的測試。
3.	如果建置結果沒問題，並且通過進一步的品質檢驗，即可結合自動化程序部署至主機發行。

從每日到每週的自動化建置，正如豐田式生產的同樣理念，儘早發生問題並即時加以解決，以避免產出不良品；儘快修正完成再繼續往前，將問題及被浪費的成本降到最低。

結論
----

程式開發是一連串的協同合作過程，因此人為疏失無法根絕；但是建立良好的開發流程，就能讓問題儘早被發現並加以修復。測試是開發流程中重要的環節，讓系統功能得到良好的驗證機制，確保開發能量能夠被累積，並加以重複利用，隨著專案的成長，偵錯的能量也會同步增長。

我們提倡在專案中實踐 TDD（測試驅動開發），只要專案有先做好規格的定義與自動化測試流程，導入「持續整合」就是水到渠成。搭配 Jenkins CI 讓專案定時、頻繁地做健康檢查，專案上線或每次更新後，就不用再太過於提心吊膽。只有開發流程令人安心，才能更專注於系統功能的完善，能夠實踐 TDD + Jenkins CI 流程的開發團隊，雖然一開始會比別人辛苦，但不久之後就會得到更多的幸福，就像隨時有個盡責的管家在一旁照料大小事。

持續整合流程從豐田式生產而來，其所提倡的核心目標是「剛剛好、不浪費」，讓流程更加透明化。有了 Jenkins 的幫忙，專案因此更有<font color="red"> “ 心 跳 脈 動 ” </font>，平時就要做好專案健康管理，否則到瀕死邊緣時，就需要徹底搶救才能回復心跳！

   [1]: http://zh.wikipedia.org/wiki/%E8%B1%90%E7%94%B0%E7%94%9F%E7%94%A2%E6%96%B9%E5%BC%8F
   [2]: http://zh.wikipedia.org/wiki/%E6%95%8F%E6%8D%B7%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91