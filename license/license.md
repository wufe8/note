https://medium.com/getamis/%E9%96%8B%E6%94%BE%E6%BA%90%E7%A2%BC%E6%8E%88%E6%AC%8A%E6%A6%82%E8%A7%80-%E4%B8%8A-45309a387c64
https://medium.com/getamis/%E9%96%8B%E6%94%BE%E6%BA%90%E7%A2%BC%E6%8E%88%E6%AC%8A%E6%A6%82%E8%A7%80-%E4%B8%8B-eeda7ce13f1e

在 AMIS 工作時經常需要使用或是修改各式各樣的開放源碼軟體，特別是在 Ethereum 生態系裡面經常會使用到的 go-ethereum。而更進一步的我們也在公司的 github 組織內釋出了許多開源專案，了解各種開放源碼授權也成為一個重要的課題。

[AMISGitHub is where people build software. More than 27 million people use GitHub to discover, fork, and contribute to over…github.com](https://github.com/getamis)

業界有許多種不同的開放源碼授權，從較為鬆散的 MIT, BSD, Apache 2.0 授權，到較嚴格的 MPL, LGPL, GPL 授權等，每種授權因為不同的背景與目的，分別定義了包含不同權利以及義務的授權條款，而這麼多選擇以及每種授權些許不同的權利義務範圍常讓工程師們暈頭轉向，開放源碼時不知道該選擇哪個授權才好。

本文將會從工程師的角度來理解以及分類各種不同的開源授權，並且從三個面向：使用開源專案、修改開源專案以及釋出開源專案三個面向來看各種授權之間有何不同之處，分成上下兩篇講解。

幸運的是自由軟體鑄造場在營運期間累積了非常多開源授權相關的文章，前輩們在這個議題留下的非常多有用的資源，本文參考了自由軟體鑄造場的法律資源，試著整理出開放源碼授權概觀，讓開發者們使用與開發相關專案時，能夠更容易理解不同授權之間的不同。

[法律源地 - OpenFoundryOpenFoundry provides essential tools and services through its service platform for users to develop Open Source…www.openfoundry.org](https://www.openfoundry.org/law-and-licensing)

```
附註：畢竟作者是軟體工程師並不是法律專業工作者，對於法律授權的理解或許有錯誤之處。若你在文章中發現任何錯誤，歡迎透過留言告知，我會儘快查證並修正錯誤。
```

# TL;DR

因為這實在是篇長文，在文章的開頭想先簡短的說明我會怎麼選擇授權。

如果是我個人的開源專案，通常會採用最鬆散的 MIT 授權，讓使用者可以自由的使用，要開源要閉源都可以，並沒有太多的限制。

如果是公司的開源專案，則會選擇定義較為詳實的 Apache 2.0 授權，跟 MIT 授權相同也允許被授權人開源或閉源使用，但在著作權規範的較為仔細，同時也規範了專利權。而因為每個國家的著作權法律都有所不同，詳細的授權也比較容易跨國使用，不會因為不同國家的預設著作權行為造成一些差異。

但如果公司的專案有引用到任何 LGPL 的授權時，我們通常都會採用 LGPL 授權，原因是因為 golang 專案通常都採用靜態連結的方式，授權為 LGPL 會讓情況比較單純一些。

希望這個說明對你來說不會太長，如果勇者如你準備好了解更多關於開放源碼授權，讓我們繼續往下吧！

# 什麼是開放源碼？

開放源碼 (Open Source) 是一種在軟體業常見的開發方式，軟體開發者透過將軟體的原始碼公開給大眾，讓其他人可以檢視閱讀、修改甚至重新散佈，其他開發者可以透過閱讀源碼更了解運作原理，進而可以改善專案並且回饋給原作者。

而作者也可以藉此獲得其他開發者的貢獻改善軟體、建立在軟體業界的聲譽，同時開源軟體與商業化並不衝突，許多商業公司背後也釋出了為數可觀的開源軟體，這些軟體依然在公司的整體業務裡面發揮作用，同時促進了整個軟體生態系的發展。

然後開放源碼並不僅僅只有「開放源碼」，根據 [Open Source Initiative 網站](https://opensource.org/osd)的定義在這邊說明三個比較重要的特質：開放源碼、自由散佈以及衍生著作。

## 1. 開放源碼 (Open Source)

![Image for post](https://miro.medium.com/max/60/1*e3zzil23CyP7doUjFcIQnA.png?q=20)

![Image for post](https://miro.medium.com/max/1492/1*e3zzil23CyP7doUjFcIQnA.png)

圖片出自於 [A new Firefox and a new Firefox icon](https://blog.mozilla.org/firefox/new-firefox-new-firefox-icon/)

最直觀的特質當然就是開放源碼了，當產品交付給客戶時開放源碼軟體會同時交付原始碼或透過清楚明瞭的方式告知可以到何處取得源碼。

## 2. 自由散佈 (Free Redistribution)

![Image for post](https://miro.medium.com/max/60/1*Ff1xnsCC35vCN0COmRFr7A.png?q=20)

![Image for post](https://miro.medium.com/max/2021/1*Ff1xnsCC35vCN0COmRFr7A.png)

除了可以閱讀源碼外，開源授權通常都授予使用者自由散佈源碼的權利，當你透過廠商或是開發者取得源碼後，你可以自由的將這份原始碼散佈給其他人而不需要經過額外許可。

一般來說就算你從合作廠商拿到商用軟體的源碼通常也是不能散佈給其他人的，而開源授權則允許你這麼做。

## 3. 衍生著作（Derived Works）

![Image for post](https://miro.medium.com/max/60/1*BlHgVo5R-IG3kD1aSrMuJg.png?q=20)

![Image for post](https://miro.medium.com/max/2398/1*BlHgVo5R-IG3kD1aSrMuJg.png)

衍生著作亦即授權可以修改源碼後衍生成另外一個產品。好比 Google Chrome 瀏覽器背後的開源專案 Chromium 被 Github 公司修改後衍生成另外一個專案 Electron 用於製作 Desktop app，而 Visual Studio Code、Brave 瀏覽器、Slack 通訊軟體以及 Twitch 桌面版串流軟體全部都是衍生於 Electron。

開放源碼軟體也授予使用者可以將此專案透過修改源碼衍生成另外一個作品。

## 其他

上面所舉的三項特質是 Open Source Initiative 所定義的其中三項非常重要的特性，而其實開放源碼授權還有許多其他定義，你可以到[維基百科上找到其他的定義](https://zh.wikipedia.org/wiki/开源软件#開放原始碼的定義)。

[开源软件 - 维基百科，自由的百科全书英语： 开源软件（ open source software ，英文 缩写：OSS，中文也称： 开放源代码软件）是一种 源代码可以任意获取的 计算机 软件，这种软件的 版权持有人在…zh.wikipedia.org](https://zh.wikipedia.org/zh-tw/开源软件)

# 有哪些授權？

在從不同層面開始講解各種授權前，我們可以用一張圖來表達不同授權的嚴謹程度。

![Image for post](https://miro.medium.com/max/60/1*vR60TufGFWZUZuDZIYfm7A.png?q=20)

![Image for post](https://miro.medium.com/max/2581/1*vR60TufGFWZUZuDZIYfm7A.png)

越左邊的授權代表在授權的規定越鬆散，反之則是越嚴格。舉例來說 MIT 授權在義務方面僅規範修改源碼後需要將授權聲明納入，完全沒有規範衍生作品是否要開放源碼，也就是衍生作品可以選擇開源或閉源，甚至改變授權也沒問題。

而最嚴格的另外一端 AGPL 授權除了規範衍生作品一定要再採用 AGPL 授權開放源碼外，就連伺服器產品沒有散佈給使用者的產品也需要依照 AGPL 開源授權並且沒有閉源的選項。

開源授權數量非常多，以下授權討論時將會針對上圖幾個比較常見的授權討論。

# 三個層面

工程師通常有幾種方式接觸或應用到開放源碼軟體，程度從輕到重分別是使用、修改以及釋出開源軟體。隨著剛開始的使用，慢慢的有可能進展到會需要修改開源軟體，或是更進一步的將自己的軟體採用開放源碼授權釋出。

就好比剛開始你可能只是個 Firefox 這個開源軟體的使用者，過了不久，你可以會發現臭蟲，修改源碼後貢獻回去，更甚至取用 Firefox 來修改成完全另外一個軟體（比如說我有聽說有人把 Mozilla 源碼改成 POS 機系統）。而到最後也有可能自行撰寫軟體後採用開放源碼授權釋出，如 AMIS 有開源釋出給 Ethereum 區塊鏈的資料索引元件 [eth-indexer](https://github.com/getamis/eth-indexer)。

這三種不同接觸到開源軟體的層面，會有不同的注意事項。

![Image for post](https://miro.medium.com/max/60/1*-R9hwE3KYkCZ7gBKs5W0Og.png?q=20)

![Image for post](https://miro.medium.com/max/1781/1*-R9hwE3KYkCZ7gBKs5W0Og.png)

## 使用

一般使用開源軟體跟其他的一般軟體不會有什麼太大的差別，比如說你使用 Firefox 瀏覽器，通常就如同一般軟體一樣，不會有什麼特殊的限制。但如果你是採用了開放源碼的函式庫就有有些需要注意的地方，通常是 GPL 系列的授權會有需要注意的地方。

這差異在於如果你連結 (Link) 了一個 GPL 授權的開源函式庫，你會有可能需要也一併依照 GPL 授權規定來開放你的源碼。這種現象稱為 GPL 感染。

如果你沒有計畫釋出你的軟體源碼，建議不要引用任何 GPL 源碼。關於 GPL 感染可以參考林誠夏的專文《[GPL 條款對於衍生程式的判定標準與其授權拘束性的擴散範圍](https://www.openfoundry.org/tw/legal-column-list/8446-the-license-inheritance-bounds-of-gnu-gpl-01)》。

另外若你的專案是 Golang 撰寫，其中 Golang 有許多專案都是採用靜態連結，根據實務上的經驗，在這種狀況下使用 LGPL 可能也會導致專案需要以相同開源授權釋出，使用 Golang 並且為靜態連結時會需要額外注意。

重點整理：

- 當你連結一個開放源碼的函式庫 (Library) 時，如果該軟體授權為 GPL，你的軟體也會需要採用 GPL 授權釋出，不論是靜態或動態連結
- 如果該軟體授權為 LGPL 並且你採用靜態連結 (Static Link) 連結該函式庫時，你的軟體也會需要採用 LGPL 釋出，但是動態連結則不需要
- 其他授權 MIT, BSD, Apache, MPL 等都不需要因此而釋出你專案的源碼

## 修改

當修改了一個開放源碼軟體時，不同的授權會有不同的規定。這些授權可以分成兩類：

- 需要開源：AGPL, GPL, LGPL, MPL
- 不需要開源：MIT, BSD, Apache

另外這些開源授權，大多都規定開源的時機在於當你「散佈」了該軟體時需要一併散佈源碼，但是如果你是架設網站讓使用者透過瀏覽器連上網站，這時候你並沒有「散佈」產品給使用者，而是使用者透過瀏覽器連結上該網站。當這種情形時，絕大部分的授權都不會要求你開放源碼，除了 AGPL 是針對這種狀況規定，如果你修改的軟體源自於 AGPL 授權的軟體，即使沒有散佈給使用者依然需要採用 AGPL 釋出源碼。

重點整理：

- 如果你修改自 AGPL, GPL, LGPL, MPL 授權軟體，散佈產品時也需要一併開放源碼
- 如果你修改自 MIT, BSD, Apache 授權軟體，你可以決定是否要開源
- 如果你的產品是個雲端服務，使用者僅是透過瀏覽器來使用你的產品時，因為沒有「散佈」行為，所以以上授權除了 AGPL 以外都不需要開放源碼

## 撰寫軟體並且以開放源碼釋出

當有一天你也決定採用開放源碼授權釋出你的軟體時，選擇不同的開源授權也會讓使用者有不同的權利以及義務。這時就可以回頭參考前面兩小節的「使用」以及「修改」來看看不同授權會有何不同的影響。

這時你可能會有另外一個疑惑，這麼多授權之間到底有什麼具體上的差異呢？在下一篇將會介紹每個授權之間細微的差別。

# 個別授權差異

## MIT 授權

https://opensource.org/licenses/MIT

MIT 授權是這幾個列出來的授權當中最鬆散的一個，在權利上面規範有授予使用、重製、修改、合併、發行、散佈再授權及販售等權利，並且可以依照需求修改 MIT 授權條款內容。

而需要遵守的義務僅有要一併散佈 MIT 的授權聲明，至於衍生物開源與否並不在義務範圍內。

MIT 授權的好處在於授權本身非常簡短，同時也沒有規範太多規則，在個人專案我通常都會採用 MIT 授權的原因也在於沒有太多規則。

重點規則：

- 散佈時要附上 MIT 授權
- 衍生作品不需要開源

## BSD 授權

https://opensource.org/licenses/BSD-3-Clause

BSD 授權有許多變形，我們這邊談論的是 3-clause BSD。BSD 授權散佈源碼以及執行檔，但是不若 MIT 一樣有明確列出其他所有權利。

所需要遵守的義務跟 MIT 一樣需要一併散佈 BSD 授權聲明並且不規定開源與否，不同處在於 BSD 授權內額外規定衍生作品不得利用軟體貢獻者的名字為其背書。

重點規則：

- 散佈時要附上 BSD 授權
- 衍生作品不需要開源
- 不得利用軟體貢獻者為衍生產品背書

## Apache 2.0 授權

https://opensource.org/licenses/Apache-2.0

Apache 2.0 授權基本上效力跟 BSD 授權非常類似，不同之處在於 Apache 2.0 授權在各個方面都提供非常詳實的授權說明，相比起來 BSD 授權則較為簡單。

在權利方面 Apache 授權針對著作權、專利授權以及商標權都有詳細的規定，著作權上允許製作衍生物、公開展示、公開演出、再授權和散佈。專利授權上允許製造、使用、販售等權利。商標權上明確規定 Apache 授權並無授權使用商標，相對於 MIT, BSD 授權並沒有明顯規範商標權來說，這樣清楚的說明不處理商標權比較明確。

在義務方面相同的需要附上 Apache 授權，並且在修改的檔案必須要附上修改聲明與一些細節的規定。

重點規則：

- 散佈時要附上 Apache 2.0 授權
- 衍生作品不需要開源
- 專利授權方面允許製造、使用、販售等多種權利
- 可為使用者提供擔保、支援服務等，但是不得使用其他貢獻者的名義擔保或背書支援服務
- 明確說明授權不處理商標權

關於 Apache 2.0 與 BSD 的差異可以參考這篇林懿萱著作的《[化簡為繁的 Apache-2.0 授權條款](https://www.openfoundry.org/tw/legal-column-list/8581-the-elaborate-license-apache-20)》。

## MPL 2.0 授權

https://opensource.org/licenses/MPL-2.0

MPL 2.0 授權比起 Apache 授權更加嚴格，若採用 MPL 授權的源碼經過修改後，必須也要採用 MPL 2.0 授權釋出。但是如果不是修改 MPL 授權的檔案，而是連結（靜態與動態連結皆可）或使用 MPL 授權的檔案，則是可以採用其他授權，也就是不需一定要開放源碼。

至於專利授權上跟 Apache 授權類似允許製造、使用、販售等權利，另外也規範了若被授權人對其他貢獻者展開專利訴訟，該被授權人原本使用 MPL 授權軟體被授予的權利將會被撤銷。

重點規則：

- 散佈時要附上 MPL 2.0 授權
- 以 MPL 授權的源碼修改後也必須要使用相同授權釋出
- 衍生作品只需要開源自 MPL 授權修改的檔案，其他部分不需開源
- 專利授權方面允許製造、使用、販售等多種權利
- 被授權人展開專利訴訟時將會被撤銷該 MPL 授權軟體賦予他的權利
- 明確說明授權不處理商標權

## LGPL 3.0 授權

https://opensource.org/licenses/LGPL-3.0

LGPL 全文是 GNU Lesser General Public License，從名稱可以得知是較鬆散的授權，不過比較的對象是 GPL，如果跟其他授權比較起來還是滿嚴格的。

首先跟 MPL 相同，如果修改了 LGPL 的源碼一律都要開源。比起 MPL 更嚴格的地方在於 MPL 授權允許你把一個 MPL 授權的專案直接放到你自己專案的目錄底下一起編譯成執行檔，但是 LGPL 授權的專案當你這麼做時會被視為 LGPL 授權的衍生作品，也需要一併以 LGPL 授權釋出。

根據 [StackExchange 上面其他人的見解](https://softwareengineering.stackexchange.com/questions/221365/mozilla-public-license-mpl-2-0-vs-lesser-gnu-general-public-license-lgpl-3-0)，LGPL 3.0 與 MPL 2.0 的差異實務上在於 LGPL 可以允許用動態連結 (Dymanic Link) 的方式將閉源專案與 LGPL 3.0 授權專案一起使用，但是如果要採用靜態連結 (Static Link) 則是會需要一併以 LGPL 3.0 授權釋出。MPL 2.0 則允許靜態連結與動態連結都不需開源。

重點規則：

- 散佈時要附上 LGPL 3.0 授權
- 以 LGPL 授權的源碼修改後也必須要使用相同授權釋出
- 衍生作品若是採用動態連結則不需要一併開源，靜態連結則需開源
- 專利授權方面允許製造、使用、販售等多種權利
- 被授權人展開專利訴訟時將會被撤銷該 LGPL 授權軟體賦予他的權利

## GPL 3.0 授權

https://opensource.org/licenses/GPL-3.0

GPL 比起前面的授權都要更加嚴格。無論是靜態或動態連結到 GPL 授權專案時，都需要相同以 GPL 授權釋出，至於其他特性則與 LGPL 3.0 相同。

重點規則：

- 散佈時要附上 GPL 3.0 授權
- 以 GPL 授權的源碼修改後也必須要使用相同授權釋出
- 衍生作品需要以 GPL 授權釋出，無論是靜態或是動態連結
- 專利授權方面允許製造、使用、販售等多種權利
- 被授權人展開專利訴訟時將會被撤銷該 GPL 授權軟體賦予他的權利

另外舊版的 GPL 2 也是目前相當熱門的授權，關於版本之間的差異可以參考林誠夏的《[GPL-3.0 與 GPL-2.0 的異同比較與應用分析](https://www.openfoundry.org/tw/legal-column-list/8753-the-analysis-of-foss-license-upgrade-based-on-gpl-30-and-gpl-20-comparison)》。

## AGPL 3.0 授權

https://opensource.org/licenses/AGPL-3.0

AGPL 是這邊最嚴格的授權，以上的所有授權在「開放源碼」的時機通常都在於當你「散佈」你的產品時需要附上源碼。但是如果像是 Google 或 Facebook 這樣的雲端服務，當你瀏覽他們的網站時其實公司並沒有「散佈」他們的產品，而是你連結到他們的網站使用他們的服務。既然沒有散佈，那就不需要開源。即使使用 GPL 3.0，只要你是類似這樣的服務模式都不會需要開放源碼。

AGPL 則是對應這樣的雲端服務而誕生的授權，就算只是使用者「利用」到自 AGPL 衍生的產品，即使產品沒有散佈到使用者手上，仍需要以 AGPL 3.0 授權。

重點規則：

- 散佈時要附上 AGPL 3.0 授權
- 以 AGPL 授權的源碼修改後也必須要使用相同授權釋出，即使沒有散佈軟體，只要有人「使用」軟體就就需要以 AGPL 開源
- 衍生作品需要以 AGPL 授權釋出，無論是靜態或是動態連結
- 專利授權方面允許製造、使用、販售等多種權利
- 被授權人展開專利訴訟時將會被撤銷該 AGPL 授權軟體賦予他的權利

# 總結

開放源碼授權真是一個龐大的課題，但是身為開發者又不得不好好的理解這些授權。不過就如同前面的 TL;DR 一樣，我自己選擇時通常有個簡單的策略來判斷專案若要開源要如何選擇專案。

你也可以了解完所有開源授權後，建立自己簡易的授權決策方針，往後要開源時就照著這個決策方針來判斷軟體要以哪個授權釋出就行了。

最後想要再次感謝自由軟體鑄造場大量的開源授權資訊，本篇文章閱讀了相當多鑄造廠發表的資料後並且整理成這篇文章。另外 2018 年 COSCUP 將會有個社群議程軌 “[FOSS Compliance — Complex Made Simple](http://blog.coscup.org/2018/05/coscup-information-about-tracks-this.html#FOSS-Compliance---Complex-Made-Simple)” 將會探討關於開源授權的相關知識，如果你想更深入了解，可以到時也到該軌議程參與。

如果有興趣了解 AMIS 的開源專案，也可以從下面的連結前往。