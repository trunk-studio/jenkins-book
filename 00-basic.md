基礎介紹
========

Jenkins CI 不是神器，它只是你的開發團隊在實踐敏捷之路的忠實管家。

可以看到每個階段都有其對應要處理的事項，而關於這些不同階段的事項所要解決的事情如下：

1.	Agile Development：有效率的溝通，做最有價值的事。
2.	Continuous Integration：自動化測試，自動化建置，讓重覆的事情可以自動執行。
3.	Continuous Delivery：讓專案可以自動發布，隨時有穩定版本可以運作，加速 test 驗證。
4.	DevOps：確保運行環境正常，負責將上述各個機制建置及維護，還有一旦 production deployment 之後的維運。

![collab](img/basic/collabnet.png)

Figure. Implement Continuous integration, Continuous Delivery and DevOps processes

資料來源：
http://www.collab.net/services/consulting


當然，實際狀況絕對不是 DevOps 這個職位的人單一可以完成上述所有的整合，必須要專案開發人員與及規劃時皆已考慮才有可能順暢的進行。

上述每一個環節都是要避免所有不必要的浪費

1. Agile Development：避免用昂貴的人力（你）無效的溝通。
2. Continuous Integration：避免用昂貴的人力（你）進行重覆測試，避免用昂貴的人力（你）進行重覆專案的建置及測試。
3. Continuous Delivery：避免用昂貴的人力（你）處理 produciton deployment 的瑣碎細節。

除了解決不必要的浪費，還有避免人為錯誤，一旦所有程序都自動化後，錯誤將容易被排除驗證。

就像[豐田式生產](https://zh.wikipedia.org/wiki/%E8%B1%90%E7%94%B0%E7%94%9F%E7%94%A2%E6%96%B9%E5%BC%8F)（TPS, Lean Production）所提倡的理念：杜絕浪費；每一次的浪費一旦被避免，也就表示有更多時間資源可以進行有價值的事！

上述內容節錄自：[企業端如何推動持續整合開發流程](http://blog.trunk-studio.com/ci_impl/)

刊登於 ithome：[【JSDC客座文章】企業端如何推動持續整合開發流程](http://www.ithome.com.tw/guest-post/98457)
豐田式生產
==========

如果想瞭解持續整合的目的，就需要先知道豐田式生產管理（Toyota Management）的概念，豐田式生產又稱為精實生產（Lean Producton）。

根據 wiki：[豐田生產方式](http://zh.wikipedia.org/wiki/%E8%B1%90%E7%94%B0%E7%94%9F%E7%94%A2%E6%96%B9%E5%BC%8F)

> 豐田式生產主要目標，是杜絕負荷過重（muri）、不平準（mura）和一切的浪費（muda）。TPS 把浪費歸納成七種：
>
> 1.	等待的浪費；
> 2.	搬運的浪費；
> 3.	不良品的浪費；
> 4.	動作的浪費；
> 5.	加工的浪費；
> 6.	庫存的浪費；
> 7.	製造過多（早）的浪費。

TPS 背後的理念是杜絕浪費，因而不再需要庫存。基本原則是「豐田模式」（The Toyota Way），概述如下：

1.	正確的流程方能產生正確結果
2.	發展員工與事業夥伴，以為組織創造價值
3.	持續解決根本問題是組織型學習的驅動力

從製造業的角度來看，能夠避免不必要的浪費跟重工，相對的效率就會變快，我們可以把 TPS 歸納的七種浪費就軟體開發的角度來看：

1.	等待的浪費，搬運的浪費：程式開發週期除了寫程式之外 build, test, deploy 都需要處理，但可以自動化
2.	不良品的浪費：程式錯誤一再發生，沒辦法杜絕，若能在每個環節測試確認，則可以確定每個動作沒有問題
3.	動作的浪費，加工的浪費：可以自動化，就不需要人的接入
4.	庫存的浪費：軟體沒有庫存壓力
5.	製造過多（早）的浪費：重覆的動作，就是一種浪費

所有在製造業所會發生的問題，大部份軟體開發也會有同樣的問題，我們可以借鏡其精神，與豐田式生產相互輝映，發展出敏捷式開發（agile），下一章節將近行介紹。
敏捷式開發
==========

說明持續整合，就不得不說明敏捷軟體開發（Agile），跟豐田式生產一樣，敏捷式開發也致力於杜絕所有可能的浪費。

參考 Wikipedia 中的說明：[敏捷軟體開發](http://zh.wikipedia.org/wiki/%E6%95%8F%E6%8D%B7%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91)

> 敏捷軟體開發（英語：Agile software development），又稱敏捷開發，是一種從 1990 年代開始逐漸引起廣泛關注的一些新型軟體開發方法，是一種應對快速變化的需求的一種軟體開發能力。它們的具體名稱、理念、過程、術語都不盡相同，相對於「非敏捷」，更強調程式設計師團隊與業務專家之間的緊密協作、面對面的溝通（認為比書面的文檔更有效）、頻繁交付新的軟體版本、緊湊而自我組織型的團隊、能夠很好地適應需求變化的代碼編寫和團隊組織方法，也更注重軟體開發中人的作用。

敏捷開發宣言
------------

- 個人與互動 **重於** 流程與工具：避免資訊的錯誤，浪費溝通的時間。
- 可用的軟體 **重於** 詳盡的文件：若詳盡的文件就是可用的軟體，可避免維護兩個地方，且文件就是運作結果本身。
- 與客戶合作 **重於** 合約協商：客戶才是需求的本身，與客戶合作將更接近目標，不會花錯力氣。
- 回應變化 **重於** 遵循計劃：唯一不變的就是變，計畫趕不上變化，如果只是不知變通的依計劃進行，往往知道方向錯了已來不及。
持續整合改善
============

有了可運行的規格以及每次異常產生的規格，接著就要讓日常累積的開發能量，能每日運行規格成為品質的後盾。

搭配 CI 定時產出報表，隨時注意專案的健康度，即早發現問題即早治療，在這要說明如何搭配 CI（Continous Integration），讓這一連串的活動能夠持續運行。

Daliy Build（or Nightly Build）
-------------------------------

1.	每天早上以及中午進行一次建置
2.	建置前需要通過所有的規格運行
3.	一旦發生錯誤，一律需要當天確認，並且當天修正完畢
4.	一旦建置完成 deploy 到 develop 機器進行測試

Weekly Build
-------------

1.	每個週末選定一天進行建置
2.	建置前需要通過所有的規格運行
3.	week build 可選擇是否 deploy 到 production 機器

每天每週的建置，正如豐田式生產一樣，發生問題即早面對並解決，避免產出不良品，修正完成再繼續往前，將異常或是浪費降到最低。

結論
----

程式開發是一連串的協同合作，人為疏失是沒有辦法根絕的，但卻可以有機制讓問題及早發現，TDD 正是一個良好的開發流程，讓開發過程包含了驗證機制，確保開發能量能夠被累積並且重覆使用，隨著專案的成長，偵錯的能樣也會同步成長。

日常有 TDD 的習慣，導入 CI 水到渠成，利用 CI 讓專案定時被健康檢查，專案上線或是更新不再提心吊膽，在令人安心的環境下開發，更能專注於系統功能的完善，我想有遵循 TDD 開發流程的團隊是幸福的，就像有爸媽呵護一樣不用擔心受怕 :)

持續整合流程從豐田式生產而來，其所提倡的核心目標是剛剛好，不浪費，以及透明，並且透過持續整合 Jenkins 的幫忙，讓專案有<font color="red"> “ 心 跳 ” </font>，若沒有正常跳動盡早急救！
Jenkins 可以在 Windows、Linux 或 Mac OS X 環境執行，一般來說我們會盡可能選擇跟 Production / Testing 伺服器接近的環境來運行。

本書範例皆以 Ubuntu Linux 演示
------------------------------

因為 Ubuntu Linux 相容多數 Open Source 軟體，也被用於許多 Production Server 環境，因此使用 Ubuntu Linux 作為 Jenkins 入門的系統，可以避免很多干擾學習的問題發生。

建議搭配 VirtualBox 虛擬機器使用 Ubuntu Linux + Jenkins，我們也為學習者提供已安裝設定完成的 VirtualBox Image，請向課程主辦單位取得檔案下載位址。

安裝 Java 軟體
--------------

建議使用 JDK 1.8 以上版本。

### 安裝 java 8 & maven

```
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update
sudo apt-get install openjdk-8-jdk
```

### 選擇 java 8 作為預設 java version

```
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

安裝 Jenkins 軟體
-----------------

參考 Jenkins 官方的 Ubuntu Linux [安裝說明](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)

```
wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```

管理 Jenkins 伺服器
-------------------

重新啟動 Jenkins 伺服器。

```
sudo service jenkins restart
```
