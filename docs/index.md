___
####**対応バージョン 2016, 2016.5, 2017, 2018, 2019, 2020**

####**Tool設定**
Maya起動バッチに以下の行を追加して起動すると、

call Y:\devtools\MayaEnvDP\ogrig2\<version>\__env__.bat

メニューに「ogRig2」が出てきます。



![](imgs/menu1.png)

___
####**== 準備 ==**
リグの生成時に大量のノード生成が行われますので、なるべくシーンが綺麗な状態で作業を始めて下さい。
理想的には新規シーンです。

モデルが存在した状態でリグを生成する時は、
モデルに"_geo"、マテリアルに"_MT"、テクスチャに"_TX"などの文字を尻に付けるなど、
名前で明確に区別できる状態にしておくのが良いかと思います。


___
####**1. スタイル調整**
**Builder**から**Import ~ Template** で基本となるスタイルを読み込みます。

![](imgs/joint_attrs_abstract1.png)

**+骨の位置合わせと軸の設定**  
骨の位置をモデルに合わせ調整したら、**[Guide Editor](guide_editor.md)**や、
Maya標準機能のOrientJointツールなどを使いつつ、センターとL側の骨の軸の向きを設定します。
<br>
※hip_style_C, leg_style_Lは水平にしてください。
<br>
軸の向きは下の設定に合わせて下さい。
スタイル骨の初期設定がこの設定なので、よく分からない時は骨の軸を表示し、
それが初期設定と大体同じか確認してみて下さい。
auto alignの部位は骨位置のみの調整で大丈夫です。
  
part       |auto align|primary axis|up axis    |world up
-----------|----------|------------|-----------|--------
spine      |yes       |            |           |
neck       |yes       |            |           |
head       |yes       |            |           |
shoulder(L)|yes       |            |           |
arm(L)     |yes       |            |           |
finger(L)  |no        |x+          |-z         |y+
leg(L)     |yes       |            |           |
toe(L)     |no        |x+          |z+         |y+

※toe => toe_style_L, toeEnd_style_L  
<br>
**+足のピボット**
軸設定が終わったら、足のピボット位置を設定して下さい。

locator             |役割            
--------------------|----------------
leg_L_piv_outer     |外側のピボット  
leg_L_piv_inner     |内側のピボット  
leg_L_piv_heel      |かかとピボット     
leg_L_piv_toe       |つま先ピボット     

<br>
<br>
**+スタイル骨のミラー**
L側の設定がすべて終わったら、ミラーリングしたい骨のルート（人型ならshoulder1_L, leg1_L）を選択し
**ogRig2->Builder->Mirror Template**でミラーして下さい。
<br>
<br>

___
####**2. リグの生成**
ルートジョイントを選択し、**ogRig2->Builder->Build Hierarcy** ボタンを押し、リグを生成します。
完了すると、このようなリグと階層が作成されます。

![](imgs/rig_fin.png)
<!-- ![](imgs/hierarchy1.png) -->
<br>
<br>
___
####**3. MCからリグへのベイク**
ogRig2 -> Animation -> MC Bake Toolを起動
アセットをリストから選択し、「bake mc->rig」にてベイクします。


<!---
**ogT → Bake MC -> Rig**で*MC2Rig*ウィンドウを立ち上げます。

![](imgs/mc2rig_win.png)

MCルートジョイント（mc_hip1)を選択後、**Bake** ボタンを押し、MC骨のアニメーションをリグにベイクします。
--->


