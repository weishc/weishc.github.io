# Vellum布料筆記

# Vellum Cloth note

Workflow：

準備衣服geo/asset → Attach cloth on T-pose → 模擬動態 → Vellum post process(auto fix bugs) → 手動修穿

1.準備衣服geo
---
for需要自己縫衣服時

drawcurve點出衣物頂點/錨點 → add將點連成線 → 各線段各自resample成subdiv cruve → planar patch from curve
- 線轉面要求是封閉的線段，無效時用fuse
- planar patch from curve要勾resample curve
- 線轉成面之前給個edit，調整衣物版型用


2.Attach cloth on T-pose
---
Method 1：
Vellum drape node
Method 2：
Vellum stich(可選) → Vellum weld → Vellum solver
- Vellum drape=time shift Vellum solver的collision 到 1F + Vellum weld
- 非布料類的配件此時縫上
- 模擬鈕扣：交互模擬RBD(WIP)詳見下方
- 分次drape時要先用post process node 把縫合的邊fuse


3.模擬動態
---
- 若要在模擬時解決穿插優先增加polish collisions數值，運算較快，接近原本的動態
- 增加smoothing iteration,collision passes也有幫助，smoothing iteration運算較慢
- post collision適用於有用布料layer功能時
- 以上參數屬於閥值，每個數值都開時增加的運算量不是疊加上去
- 耗時上，2 substep*10碰撞疊代約等於1 substep*20碰撞疊代，但前者效果會更好 [來源](https://www.sidefx.com/docs/houdini/dyno/vellumtips.html)
- 初始constraint iteration數值可用模型相距最遠兩點之間的邊數去估算 [來源](https://www.sidefx.com/docs/houdini/dyno/vellumtips.html)


4.Vellum post process(auto fix bugs)
---
- 模型和布料的subdivision type用loop較適合
- 不影響畫面時可以用detangle，但衣服有穿插時用detangle會更嚴重，關掉self collisions可減少
- detangle的thickness開太高會使衣服產生和模型佈線相同的皺褶，細分沒用，若較高的thickness有必要，用兩個post process，先detangle再細分
- 開self collisions有助於找穿插
- 用volume sample+模型的N找出穿插，配合detagle SOP和delta mush SOP修復
- 修復時先blast出穿幫區域，勾選delta SOP中的 pin border，再fuse回去


5.手動修穿
---
mix vop設key

模擬鈕扣(WIP)
Method 1：RBD
需模擬兩次vellum，Vellum → RBD → Vellum
Method 2：Vellum softbody structure
硬度開超高假裝成鋼體，但不能在縫製衣服階段用，weld會破壞結構

絲綢,牛仔布料,皮革：https://www.sidefx.com/tutorials/h17-vellum-cloth-lookdev-tips/


