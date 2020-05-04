#本日の実習内容
##論文購読
Geller & Ohminato (1994, GJI) 第２章
##実習（予定）
1. SPC_SAC.propertiesの中身を説明
2. 仮定した地球内部構造（1次元; 半径rのみの関数）をプロット
3. Record section（地震波形記録を震央距離や方位角順に並べてプロットしたもの）の作成

---
---

# 実習
[Skype会議](https://join.skype.com/YsHD0ReeJ1xa)15:30~

##1. SPC_SAC.propertiesの中身
```
manhattan SPC_SAC
##Path of a working folder (.)
workPath /mnt/lasagna/suzuki/Ensyu2020/working/DSMrun
##SACComponents for write (Z R T)
components Z R T
###If you do NOT want to use PSV or SH, you set the one 'null'.
##Path of a PSV folder (.)
psvPath .
##Path of an SH folder (.)
shPath .
##String if 'modelName' is PREM, spectrum files in 'eventDir/PREM' are used.
##If it is unset, then automatically set as the name of the folder in the eventDirs
##but the eventDirs can have only one folder inside and they must be same.
modelName MIASP
##Type source time function 0:none, 1:boxcar, 2:triangle. (0)
##or folder name containing *.stf if you want to your own GLOBALCMTID.stf 
sourceTimeFunction 0
#SamplingHz (20) !You can not change yet!
samplingHz
#timePartial If it is true, then temporal partial is computed. (false)
timePartial
```

\*source time function (震源時間関数): モーメントの時間変化. これを畳み込むか否かのパラメータ. ここでは0を選択.
\*modelNameはDSMの計算に用いた地球内部構造モデル
\*SPC_SACを実行する際には以下のようなファイル構造が必須.
```
.
│
│spcsac.properties
│
│—201506231218A ------------------------#イベントIDごとに分類
│        │
│        │ MIASP_PSV_4rs.inf -----------#DSMの入力ファイル
│        │ MIASP_SH_4rs.inf  -----------#DSMの入力ファイル
│        │
│        ├─MIASP -----------------------##DSMの出力結果を格納. ディレクトリ名は内部構造モデル
│        │   │
│        │   │*PSV.spc -----------#DSMの出力ファイル
│        │   │*SH.spc -----------#DSMの出力ファイル
│        │   │
```

---
---

##2. 仮定した地球内部構造（1次元; 半径rのみの関数）をプロット
サンプルコードの場所：/mnt/lasagna/suzuki/Ensyu2020/structure/scripts

1. MIASP_PSV.polyのようにDSMのインプットファイルの構造のみを取り出したファイルを用意する. 
2. `./structure.sh MIACP_PSV.poly`で実行&出力. その際invmkfunc.shも必要.
3. dVpVsRho.pltの中身を書き換えてyrange, xrange等を変えてプロットしてみる.
4. `gnuplot dVpVsRho.plt`で実行
5. `evince MIASP_PSV.eps`で出力
6. 以下のような図が得られる
![IMAGE](resources/920C63DE0BC867169EE95BCA212025A4.jpg =661x1061)

---
---

##3. Record sectionの作成準備
サンプルコードの場所：/mnt/lasagna/suzuki/Ensyu2020/recordSection/recordSection.sh

/mnt/lasagna/suzuki/Ensyu2020/DSMrun/manyStationsをコピーしてDSMを実行しておくことが前提条件です. このディレクトリの直下に201506231218Aのディレクトリがあります. 計算を行うときは、201506231218Aに移動して実行してください.  出力先のディレクトリ(MIASP4RS)も用意しているので、その中に出力されます. 出力された*.spcはSPC_SACでSAC形式に変換してください. Record section作成の詳細は次回に行います.

---
---

##課題