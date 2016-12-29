# What is Fractals?
フラクタルとは数学者ブノワ・マンデルブロが提唱した幾何学の概念である．自己相似性をもち，どこを拡大しても自分と同じ形が出てくる．
自然界にも多くの形を見ることができる．
非常に美しい形をみることができ，コンピュータを用いたアート作品としても大きく発展した．ここではいくつかのレンダリング手法を紹介する．

近年発見されている高速なレンダリング手法は，その他のフラクタルレンダリングの手法との関連が非常に深い．主題はクライン群であるので，のちのいくつか重要な概念を紹介しておく．
クライン群の円列はマンデルブロがマンデルブロ集合を提唱する以前から存在はしていた．
# Escape Time Fractals
マンデルブロ集合やジュリア集合に代表されるフラクタルである．このタイプのフラクタルは，特定の漸化式を繰り返し計算し，その漸化式の収束，発散を見ることで色を付ける．
例えば，マンデルブロ集合では，複素数平面上の点c全体に対して，
$$ z_{n+1}=z^2_{n} + c z_0 = 0$$
で定義される漸化式を計算し，$$z_n$$が無限大に発散しないものをマンデルブロ集合と呼ぶ．

グラフィクス性能の向上により，GPUを用いたレンダリングを容易に行うことができる．
よく行われるのが，OpenGL Shading Language(GLSL)やHigh Level Shading Language（HLSL）のフラグメントシェーダを用いた方法である．
フラグメントシェーダは本来，ポリゴンに陰影をつけるために使用されるが，スクリーンスペースに矩形のポリゴンをレンダリングすることで各ピクセルごとの処理を記述し，図形をレンダリングすることができる．先に説明したEscape Time Fractalはそのまま並列化することができる．
距離関数を用いることでレンダリングを行う．

距離関数とレイマーチングという手法を用いて三次元形状をもつフラクタル図形を描画することも盛んにおこなわれるようになった．
フラグメントシェーダを用いた画像のレンダリングでは，その性質上，描画したい図形までの最短距離を返す距離関数が用いられることが多い．フラグメントシェーダでは，各ピクセルごとに，その点が図形に属しているか計算することで描画することができる．
陰関数から微分を用いて近似的に距離を求めるDistance Estimationという手法がある．これはこのサイトが詳しい．著者のInigo Quilez氏は
http://iquilezles.org/www/articles/distance/distance.htm
この方法とGreen Functionと呼ばれるマンデルブロ集合の陰関数を用いることでマンデルブロ集合までの距離を求めることができる．より綺麗にレンダリングすることができる．
http://iquilezles.org/www/articles/distancefractals/distancefractals.htm

距離関数は二次元だけではなく，三次元空間でも用いることができる．三次元形状をシェーダでレンダリングするためにはレイマーチングという手法を用いる．
レイの先端を距離関数で得られた最短距離だけ先へ進めることを繰り返し，近似的にレイと物体との交差点を見つける手法である．
詳しくはここでは述べないが，Web上には多くの学習コンテンツが公開されているため，学ぶことは容易である．二つあげておく．
https://wgld.org/d/glsl/
http://www.demoscene.jp/?p=811

マンデルブロ集合を三次元に拡張する試みは多く行われてきた．例えばRay Tracing  Deterministic 3-D Fractalsなどがある．しかし，マンデルブロ集合のような豊かな形状は得られなかった．
その中でも後述する可視化されたクライン群の一種であるQuasi Fuchsian 3D Fractalは大きな影響を与えたと言われている．
その後2009年にmandelbulbが生まれた．
mandelbulbに関する歴史はこのサイトが詳しい．
http://www.skytopia.com/project/fractal/mandelbulb.html
これを機に三次元フラクタルの議論はさらに盛り上がり
mandelboxと呼ばれる形状も開発される．
https://sites.google.com/site/mandelbox/what-is-a-mandelbox
これらの詳細なレンダリング手法はSyntopiaの記事が詳しい．
http://blog.hvidtfeldts.net/index.php/2011/06/distance-estimated-3d-fractals-part-i/
基本的には，Escape timeと同様のアプローチである．

これらのレンダリング手法はFractal Forumsで発表，議論されている．


# Fractal Frame
Iterated Function Systemと呼ばれるアルゴリズムを用いてレンダリングされる
各種の点に様々な関数を適用し，その集積点をレンダリングする方法である
Fractals EverywhereはIFSによるフラクタルの研究を広めた書籍である．
The Fractal Frame Algorithmが詳しい．
GPUによる並列計算を利用したレンダリング方法も提案されている．


# Softwares
- Ultra Fractals
- Fractal Science Kit
- Apophysis
- Mandelbulb 3D
- Mandelbulber
- fractal lab
- flux

# Other Fractals
## 3D fractals
- [Ray Tracing  Deterministic 3-D Fractals](http://delivery.acm.org/10.1145/80000/74363/p289-hart.pdf?ip=133.26.34.248&id=74363&acc=ACTIVE%20SERVICE&key=D2341B890AD12BFE%2EDE682B34580D1A94%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&CFID=880607056&CFTOKEN=24845145&__acm__=1482648511_561db24c3d8e428ce5ac25865fbaa34e)  
John C. Hart, Daniel J. Sandin, Louis H. Kauffman(1989)

- [RAY TRACING OBJECTS DEFINED BY SWEEPING A SPHERE](http://www.sciencedirect.com/science/article/pii/009784938590055X)  
J.J. Van Wijk (1985)
- [RAY TRACING FOR CURVES PRIMITIVE](http://wscg.zcu.cz/wscg2002/Papers_2002/A83.pdf)
Koji Nakamaru, Yoshio Ohno (2002)

- [The Fractal Frame Algorithm](http://flam3.com/flame.pdf)  
Scott Draves, Erik Reckase(2003)
- [High Performance Iterated Function Systems](https://jo.dreggn.org/home/2010_fractal_flames.pdf)  
Christoph Schied, Johannes Hanika, Holger Dammertz, Hendrik P. A. Lensch (2010)
- [GPU-Accelerated Iterated Function Systems](http://www.geocities.ws/simesgreen/gpuflame/GPU_ifs_final.pdf)  
Simon G. Green
## Books
- Fractals Everywhere  
Michael F. Barnsley

