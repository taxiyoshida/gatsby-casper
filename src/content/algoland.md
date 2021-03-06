---
title: "MITのCS, ゲーム理論家集団が生んだ暗号通貨 Algorand"
author: Ghost
tags: ["Getting Started"]
image: img/marvin-meyer-794521-unsplash.jpg
date: "1922-12-12T10:00:00.000Z"
draft: false
---

# Tl;DR
MITのCSとゲーム理論の専門家が結集したAlgorandのビザンチン合意プロトコルは既存のプロトコルの課題を超えている可能性があるが、保留されている誘因設計が吉と出るか凶とでるかが、その価値を分けることになる。

※小難しい解説が大変だという方は「3.2 ラーメン一蘭合意」と結論を読んでいただければ大体わかる。特に一蘭は最高傑作のたとえ話である。
# 1. 経緯 

Algorandの始まりはSilvio MicaliとJing Chenの論文”Algorand Agreement - Super Fast and Partition Resilient Byzantine Agreement”である。これが2016年に発表され、2018年2月に400万ドルを集めAlgorandは正式に企業として登録された。2018年7月にテストネットが稼働し、今年の10月、6200万ドルを集めた。12月にはAlgorand プロトコルを採用する事業に投資するためのファンド”Algo Capital”を設立した。

Algorandプロトコルを共同開発したSilvio Micaliはチューリング賞受賞のMITコンピュータサイエンス教授であり暗号学者。Micaliは証明者の主張が正しいこと以外の情報を検証者に漏らさない証明の手段である「ゼロ知識証明」の共同発明者の一人であり、公開鍵暗号、検証可能擬似ランダム関数、デジタル署名、紛失通信プロトコル、セキュアマルチパーティーコンピュテーションに関する研究で最もよく知られている。

2016年のAlgorandに関する最初の論文の共同執筆者であるStony Brook Universityアシスタント・プロフェッサーJing Chen(現Head of Theory Research and Chief Scientist)はMITでCS博士号を取得したAlgorithmic game theory (アルゴリズム的ゲーム理論)の専門家。アルゴリズム的ゲーム理論とはゲーム理論とアルゴリズム理論の融合領域で戦略的環境におけるアルゴリズムを設計・解析することを目的とした理論であり、経済学とコンピュータサイエンスの交差点とも言える領域に属している。同社の幹部とアドバイザーにはこのアルゴリズム的ゲーム理論のほか、暗号学、マクロ / ミクロ経済学、分散システム、ネットワークを専門とするMITの教授、出身者の面々が名を連ねている。経営部分を担当するCEO、COO、CTO、エンジニアリング、プロダクト、HR、マーケティングには企業でキャリアを積んだベテランが雇われている。

# 2. 既存アルゴリズムとの比較

MicaliがAlgorandを提案する文脈を知るため、合意アルゴリズムがたどってきた経緯を振り返ろう。合意アルゴリズムはブロックチェーンよりずっと前から存在していた。分散システムで一貫した結果を生むアルゴリズムはすべて「コンセンサス(合意)アルゴリズム」と呼ばれる。これまでにも多くの合意アルゴリズムが使用されているが、多くは悪意のある攻撃者を想定しないモデルだった。

悪意のある攻撃者を想定する分散合意の問題が、ビザンチン将軍問題である。中央の管理システムが存在せず、参加者の中に故障したコンピュータや悪意を持った個人が紛れ込んでいる状態で、全体で正しい合意を形成できるのか。この問題に耐性をもち合意を成し遂げられる性質のことをビザンチン障害耐性(Byzantine Fault Tolerance: BFT)と呼ぶ。

よく知られているPaxosアルゴリズムでもビザンチン問題に対処できるし、Paxosの改善されたバージョンが公開されている。ただし、多くのBFTプロトコルはヘビーな通信が必要であるため、多数の参加者に対応できない。PoWのようなブロックチェーン合意アルゴリズムでは、多数の参加者を想定しており、トランザクションごとの対話が少なくて済むが、一貫性が保証されるのではなく、より制限の少ない確率的なモデルが採用されることがよくある。

合意アルゴリズムには以下の4つの分類がある。下の項目に進むほど難易度が上がる。下の2項目を「ビザンチン合意」と呼ぶ。

* 既知の参加者、非ビザンチン障害耐性：Paxos、Raft
* 未知の参加者、限定的な攻撃モード：Chordおよび他の分散ハッシュテーブル
* 既知の参加者、ビザンチン障害耐性：PBFT(Practical Byzantine Fault Tolerance)、UpRight、Byzantine Paxos
* 未知の参加者、ビザンチン障害耐性：プルーフ・オブ・ワーク(PoW)、プルーフ・オブ・ステークス(PoS)

多くのBFTはノードの母集団を事前に”知っている”ことを想定している。通常、ブロックチェーンアルゴリズムはこの仮定をせず、参加者はいつでも参加できる。つまり、区分の一番下、PoWとPoSは多数で未知の参加者、しかも悪意の参加者を含むなかでの分散合意を成し遂げたのことが画期的だった。Bitcoinとはビザンチン合意を金融取引に応用したものであり、金融機関という信用を提供する”Trusted third party”(信頼される第三者)を必要としない、”価値移転を可能にした。Bitcoinはサードパーティに依存せずプロトコルに従い、ステークホルダーのふるまいで継続し続けた。採掘者にとっては、P2Pネットワークを攻撃するよりも採掘(コンピュテーション資源を投入し新しいブロックを生成するための競争をすること)することの方が儲かるのだ。2009年にBitcoinが登場しやがて中国山間部に信頼の置けない採掘者の集団が生まれた後もPoWはBFTを実証し続けたのだ。だが、PoWには課題があった。

# 2.1 PoWの課題

PoWの欠点とは、ひとつは余りにも無駄なコンピューテーションリソースと電力を投入されていることだ。PoWは採掘者にハッシュ関数の”SHA-256”を利用した問題を解くことを求めている。それは32ビットの値である”nonce”をSHA-256に入れ、出力される値が求められる条件を満たすかを探るクイズである。採掘者にとってこのクイズを解く最適な手段は”総当たり方式”である。Bitcoinの法定通貨建て価格が高騰するに従い、総当たり方式に最適なコンピュータを作るインセンティブが生まれている。

価格が下落した現在はそうでもないが、一時期は採掘者が寒冷な地域にある余剰電力のある水力発電所の近くに多量のASICとともに殺到するできごとを引き起こした。一部の暗号通貨の採掘にGPUが適していたためGPUが品薄となり、機械学習、コンピュータグラフィックスやAR / VRなどに取り組む人たちにリソースが回らないという社会的損失をもたらした。もうひとつはコンピューティングリソースの投入量とスループット(機器や通信路などが単位時間あたりに処理できる量)が相関しないことだ。Bitcoinのスループットは10分に1回の1MBのブロックに限定されているが、価格がピークの2017年12月には途方もないコンピューティングパワーが”廃棄”されていた。

PoWはハッシュパワーの51％を超える単一、あるいは共謀した採掘者の攻撃に脆弱である。近年は採掘者の寡占化が進んでおり、サトシ・ナカモトが残した遺産を基にビットコインを開発する開発者との溝が深まっていた。特に最大の採掘者であるBitmainはアルゴリズムの穴を突いて不正なハードウェアアクセラレーションをしたり、販売しているマイニング用ASICにバックドアを仕込んで競争相手のマイニング能力を操作したり、チェーンを枝分かれさせ、自分にとって好ましい新しい”Bitcoin Classic”を生み出したりした。

この通りPoWは分散合意を成し遂げたが同時に高いコストを作った。欲張りな人は低いコストでの不特定多数間のビザンチン合意がほしいと思うだろう。それで、より高いスループットを必要としていたEthereumを筆頭に多数のプレイヤーがもともと議論が存在したプルーフ・オブ・ステーク(PoS)に注目するようになる。直訳すると”賭けの証明”ということになる。

# 2.2 PoSの利点と課題

PoSは「あなたがどれだけ賭けたかに基いた確率で報酬を獲得できる仕組み」だ。あるいは「あなたが新しいブロックを生成する権利を獲得する確率が、コインの持ち分に応じて変化する」仕組みである。(この記事で詳述した。[『”独占戦略"に脆弱な分散合意アルゴリズム「Pos」』](https://axion.zone/pos-vulnerable-to-monopoly-strategy-by-large-holders-jp/)) 

PoSは持ち分に応じて投票するだけなので、PoWの課題であるクイズを解くための軍拡競争が起きない。PoWはBFTを確保するためさまざまな”儀式”を織り込んでいるが、PoSは投票と承認のプロセス、そしてその報酬の分与だけなので、コストが低い。

また、PoWで指摘したビッグプレイヤーが行儀の悪いことをする可能性を排除できているという想定をしている。PoSでは大量のコインを持っている参加者が検証プロセスにおいて悪意のある行動を起こす動機がないと想定する。なぜなら多量のコインを保有する「金持ち」は確実により金持ちになれるのだから偽りの行動をする誘因に欠けているためだ。お金持ちが次のブロックを生成する人になれる確率が高く、もたらされた報酬がお金持ちにさらなるお金をもたらすからだ。ビザンチン合意のシミュレーションでは自己利益の最大化を目指す利己的主体を想定する。これによりステークを持つ主体はそのステークを手放さず、投票に参加する誘因があると想定できる。PoSはこれが合意に安定をもたらすと想定する。

もうわかった人もいると思うが、PoSには明確な脆弱性がある。独占戦略だ。賭けたステークに基づいて確率的に報酬が配分されるのなら、他者を押し出すために自分が必要な額以上を賭ける”攻略法”がある。この攻略法はゲーム理論が想定する利己的主体というプレイヤー像とフィットする。市場価格より高い価格でコインを値付けして買収していけばいくほど、PoSの結果生み出される報酬を獲得できる確率が拡大していく。プレイヤーに正直な投票をする誘因のために報酬を設定したはずなのに、その報酬と報酬の分配メカニズムが他者を追い出す戦術の誘因を生みだしてしまうわけだ。この[『サトシコンセンサスの次、Algorandの挑戦』](https://axion.zone/algorand-cryptographer-silvio-micali/)でMicaliはその点に言及している。


# 2.3 ”失敗したPoS”の先行例

NemをPoSコインと類似する実験と捉えてみよう。Nemの「重要度スコア(importance score)」に基いてコインを分配するプルーフ・オブ・インポータンス(PoI) は、PoSの類似例である。PoIでもコインの保有量が一番大きな要素であり、大量保有者は少量保有者よりも著しく効果的にコインを増やせるのだ。Nemでは、PoI が生みだす収益のほとんどを大量保有者が飲み込んでおり、いわゆるマルチ商法と同様の構造で、大量保有者にはNemネットワーク(ネットワーク商法のネットワークではないよ)の重要な役割が優先的に付与されるようになっていた。そして保有者たちのメカニズムへの理解は、コインの保有量と比例するのだ。

大量保有者は積み重なった大量のコインを法定通貨に換えたい。ただNeｍの通貨Xemは傍流で安かった。大量保有者は情報の非対称性を活かし新規参入者にNemの”利点”を説得し、取引所での購入を勧めた。新規参入者には取引所での法定通貨との交換レートを引き上げる役割が期待されていたのだ。新規参入者はこのメカニズムに組み込まれるとほどなく状況を理解し、利益を得たいがため、より”新しい新規参入者”を呼び寄せるようになった。だまされた初心者の大群が価格を高騰させると、大量保有者は保有コインの一部を高値で売ることができた。大量の売りで価格が急落し、高値づかみの新規参入者は大損をした。「モラルハザード」である(詳細はこちらの記事で。[『”独占戦略"に脆弱な分散合意アルゴリズム「Pos」』](https://axion.zone/pos-vulnerable-to-monopoly-strategy-by-large-holders-jp/))。

ここで、興味深いのは、暗号通貨取引所という存在は、法定通貨との交換可能性を提供するため、攻撃者が不正を働くインセンティブを著しく高めていることだ。余談だが、史上最大のクラック案件となったCoincheck事件では、盗まれたXem(Nemのトークン)はクラッカーがダークウェブに自ら構築した取引所で法定通貨と交換された。暗号通貨と法定通貨の交換レートが生じるためPoS通貨ではこのようなモラルハザードも想定できるだろう。PoSにもPoIと同じエコノミクスが働いているので、同様のスキームが起こる可能性がある。法定通貨で儲けることを目的としなければ、独占、あるいは共謀を含みにした複占、寡占をすればPoSはいとも簡単にクラックできる。

Ethereumはこの可能性を織り込んでいるが不十分である。EthereumはPoSの採用に伴い多数派を形成して不正なトランザクションを承認させようとしたり、共謀の兆候があるプレイヤーを検出し罰するアルゴリズムの採用を検討している。Micaliは会社設立時のインタービューで罰の活用に否定的な考え方を話している。「脆弱な国家は脅威と恐怖で支配を行います。なぜ、ある国では犯罪と戦うために残酷な刑罰を課すことにしているか、というと、犯罪者はめったに捕まえられないからだ。悪い行為をした人を追放したいと思うはずですが、よく作り込まれたシステムは、人を罰する必要がないシステムです」。この「アメとムチ」というのはメカニズムを維持するために採用する古典的な手段であり、最悪の中の最高とも言うべきだろう。市場設計をする人ならば「アメとムチ」ではなく、罰ではなくプレイヤーと自然と好ましい誘因に沿って行動することを促す優れたメカニズムを設計するのは前提とも言えるだろう(関連記事[『ナッジ: パターナリズムでもリバタリアニズムでもない社会設計』](https://axion.zone/nudge-libertarian-paternalism/))。また、この記事[『Googleの検索広告で学ぶオークションの理論と実践』](https://axion.zone/If-you-wanna-know-gafa-learn-auction-theory/)ではオークションを通じてこのようなメカニズムデザインについて検討しているのでぜひ読んでほしい。

EthereumはPoSへ移行すると言われるが、執筆時点ではまだPoWにとどまっている。Bitcoinは1秒あたり7トランザクション、Ethereumは1秒あたり15トランザクションしか処理できない壁にぶつかっている。Bitcoinにもライトニングネットワークという解決策があるが、これも様々な問題点が現れたため開発の経過は難航している。両者は現状、明らかにスケーラビリティ(拡張性)がないのだ。

もとから既存金融機関の利用を念頭にいれたRippleは信頼できる一部の承認者(validator)による投票で取引を承認できるようにしている。この記事の序盤で指摘した、既知の参加者、非ビザンチン障害耐性の最も古典的な合意アルゴリズムを採用していることになる。これによりRippleは取引を承認するまでにかかる時間が3~6秒と高速化しており、BitcoinとEthereumよりもスループットは遥かに大きい。Rippleでは単一の承認者だけが悪意を持ったとしても、システム全体を破壊することはできないが、過半の承認者が悪意を持てばシステムを破壊できる。Rippleは運営と開発を行うRipple社がすべてを管理しているプルーフオブオーソリティ(PoA: 権威による証明)と大差がない。Rippleは拡張性は確保したがビザンチン合意を放棄した。

つまり、ビザンチン合意と拡張性はトレードオフになっている。裏を返せば、このトレードオフを乗り越えれば、いままでにない暗号通貨が生まれるわけだ。AlgorandはPoSの暗号学的、ゲーム理論的な改善によりこのトレードオフを解決しようとしている。では、ついにAlgorandの本体の仕組みを説明しよう。

#  3. Algorand Protocolの実施形態

Algorandはリーダーによる選挙を伴うシンプルなビザンチン合意のプロトコルである。正直なユーザーが多数派(2/3以上)であることを条件としている。Algorandのビザンチン合意は、バリデータ(検証者)の検証時間を完全に同期させる必要がない。バリデータには他社の存在を知らないまま瞬間的な同意を求める瞬間合意アルゴリズムが適用されている。

Algorandは以下のステップを採用している。

1. ランダムに選択されたユーザーがリーダーとなり、新しいブロックを提案して循環させる。
2. ランダムに選出された複数ユーザーによる委員会が設置される。
委員会はリーダーから提案されたブロックに関して2/3以上の賛成投票によりビザンチン合意に達する。
3. 合意されたブロックは委員会メンバーによりデジタル署名される。
4. デジタル署名は参加者全員が新しいブロックについての確証をもてるよう参加者によって回覧される。署名者の信用証明書の回覧をだけでなく、ハッシュ値が確定するとハッシュ値も回覧され、参加する誰もが新ブロックについて知ることが保証される。

*※選出されたリーダーが偽りのブロックを提案した場合、委員会がブロックを否決し、新たにリーダーを選び直すステップに入る。*

最初のブロック生成をする”リーダー”とそれを検証(Validate)する”委員会”のメンバーは秘密裏にランダムに選ばれる。リーダーと委員会のメンバーは匿名の状態で、一時的にあてがわれた公開鍵だけが回覧される。委員会のメンバーはプロトコルとの通信はあるが、他のメンバーが誰かは知らされないまま投票に入る。承認後のブロックのデジタル署名と信用証明書(Credidential)の回覧により、承認の正しさが確定する。参加者による逐次設定される”委員会”への監視が働くことになる。

Algorandプロトコルはブロックがネットワークを伝播する間に提案されると同時に、ブロックに対する合意プロセスを進める。即時合意(Instant Consensus)である。ユーザーはブロックを受け取った瞬間にブロックに投票することを要求され、その間もブロックは残りのユーザーに伝播し続ける。すべてのユーザーがブロックを見た時点で、すべての投票が完了しているのだ。入り組んだDPoSとは異なり、1回の投票で合意に達する。伝播後、複数回の投票の後に追加の作業を必要とする従来のメカニズムとは対照的だ。この即時合意は、新しいブロックが正しく伝搬されることを前提としている。悪意のあるブロック提案者が現れるケースでは、プロトコルは悪意のプレイヤーであることを認識するとそのプレイヤーを無視してすぐに新しい提案者の選択に進む。

# 3.1 ”暗号化されたくじ引き”とGossip Protocol

ブロック提案者と委員会を選定する手段を”Cryptographic sortition(暗号化くじ引き)”という。ほとんどのPoSシステムはある種のランダム性に依存しているが、Algorandは自分のコンピュータで”宝くじ”を実行して自己選択するという点で他のアルゴリズムとは異なるとMicaliは主張する。宝くじは過去のブロックのデータに基づくが、選択は参加者同士のメッセージ交換を伴わず自動かつ完全にランダムである。Micaliは古代ギリシアの都市国家アテナイで採用されていた直接民主制の手法である”sortition”(くじを引いて選択する行為)から命名したという。先述したDPoSが「間接民主制」ならAlgorandは「直接民主制」であるという含意があるとみられる。

Cryptographic sortitionは、verifiable random functions (VRFs) で行われる。VRFsは検証可能疑似乱数関数と訳される。疑似乱数関数とはある出力があったとき、一見ランダムに作られた数列のように見えるが、実際には決定論的な計算によって求められている数列を出力するものだ。ここに「検証可能性」が加わることで、VRFsには擬似乱数を正しく生成したことを示す証明を出力するもうひとつの特徴がついている。公開鍵を参加者の間で回覧した際に、VRFsのおかげで参加者には、その疑似乱数が秘密鍵から正しく生成したことは証明されるが、その秘密鍵の情報は渡さないで済む。これは、ブロック提案者と委員会メンバーを特定し連絡する機会を奪いながらも、参加者全員に承認プロセスが正規のレールの上で行われていることを知らせる手段である。同時に沢山のID(ユーザ)を作り投票への影響力を行使しようとするシビル攻撃などの攻撃への耐性を高めてもいる。MicaliはこのVRFsの作者の1人である。VRFsはDefinityなど他のブロックチェーンプロジェクトでも採用されている。

cryptographic sortitionが選定した委員会がブロックをベリファイした後は、Gossip Protocolで新しいブロックを伝播させる。

￼![Screen Shot 2018-12-21 at 13.01.48](//images.ctfassets.net/4l4ail9691ba/5pRtf8NDVYOS82uQs8OKUk/4cb13ac013ac58b2d1fda68fbb2fc0dd/Screen_Shot_2018-12-21_at_13.01.48.jpg)

Figure 1: Via “Algorand: Scaling Byzantine Agreements for Cryptocurrencies”

Gossip Protocolとはピアが自身や他のピアの状態に関する情報を定期的に交換するP2P通信プロトコルである。ランダムに選んだ相手と情報を交換し、自身が持つデータの更新を繰り返す。システムの参加者が不定期的に増減して全体を把握できない状況や、一時的に通信できない場合でも情報を伝搬できる。

![Screen Shot 2018-12-21 at 16.08.11](//images.ctfassets.net/4l4ail9691ba/198iHYTXH20igI2O8meoi4/e1544b68174105de43a7cdeb367a7109/Screen_Shot_2018-12-21_at_16.08.11.jpg)￼
Figure 2: An overview of transaction flow in Algorand. Via “Algorand: Scaling Byzantine Agreements for Cryptocurrencies”

メッセージが偽造されないようにするため、すべてのメッセージは元の送信者の秘密鍵で署名されている。 他のユーザーはメッセージを中継する前にその署名が有効であることを確認する。先述したようにVRFsは与えられた公開鍵が秘密鍵から正しく生成されたことを証明してくれている。グラフ構造の中で転送ループを回避するために、ユーザーは同じメッセージを2回中継しない。 AlgorandはTCP上でゴシップを実装し、所持金の量に応じてピア選択の重み付けをする。

# 3.2 ラーメン一蘭合意

おそらく難解だったはずなので楽しい「例え話」を用意した。あなたはラーメン「一蘭」をご存知だろうか。客が食べる場所に仕切りが用意され、他人とのコミュニケーションが断たれているラーメン屋だ。十分に理解できた人にとってはたちの悪い冗談なので読み飛ばしたほうがいいだろう。

ラーメン「一蘭」には調理人がいない。客が調理するシステムである。店の真ん中には宝くじのマシンがある。このくじマシンは暗号学を使って悪さができないようになっている。くじで選ばれた客が調理人になる。調理人はラーメン(ブロック)を調理する。次にくじは店の外に並んでいる客の大群からランダムに食べる客を選ぶ。この客は委員会を組織してラーメンが提供されるやいなやその瞬間に食べる(提案が正しいかを検証し投票する)。食べて問題がなければ「うまい」といって署名して承認する。

このラーメン屋で大事なのは、秘密のうちに調理人と客をランダムに選んでしまうことだ。客は仕切りのせいで他の客が誰かはわからないし、他の人との連絡は基本禁じられている。いきなり「誰かがラーメンを作り始めましたよ」というメールが皆のスマホに届く。「ラーメンの調理者は●●さんです。そのラーメンが美味しかったと委員会で投票して賛成が得られました。ラーメンのお味と委員会の署名をここに記します」という証明書が届く。この証明書のときだけは、仕切りから身を乗り出して隣の客に手紙を見せてあげることが許されている。でもふたつ隣の客に見せるのはだめだ。この証明書が終わると客は外に出て、くじの選定を待つことになる。ふりだしに戻る。

![nishidori 6](//images.ctfassets.net/4l4ail9691ba/1bIfx3Y470yKigIUSsGuIw/8067b9f915af16c31dda2add77745414/nishidori_6.jpg)

Fig03 ラーメン一蘭、Via ichiran.com

不思議なようだけど、この繰り返しでラーメンが一蘭のラーメンにふさわしいことが承認されるのだ。あとはこのプロセスを繰り返し続ければ、一蘭の客たちはお互いの帳簿を管理できるのだ。ラーメンが作られ食べられる、ラーメンが作られ食べられる……堅牢なビザンチン合意のできあがりである!

いかがだったでしょうか?

# 3.3 性能は”Bitcoinの125倍”

さて、冗談はここまでにして、次は性能だ。論文はAmazon EC2 VM1000インスタンスで実行された実験結果では、Algorandは最大22秒に5万ユーザーが合意した1Mのトランザクションを格納したブロックを処理したと主張した。レイテンシが最も低い場合には22秒で2Mバイトのブロックを処理したと主張する。1時間に327 Mのトランザクションをコミットするようだ。 Algorandはブロックサイズが大きくなるにつれてスループットを向上させるが、レイテンシはいくらか増加するに留まる。たとえば10 MByteのブロックサイズでは、Algorandは1時間あたり約750 Mのトランザクションをコミットする。これは1時間に6MのトランザクションをコミットするBitcoinの125倍だ。

また論文はこの実験でユーザー数を50万まで引き上げてもレイテンシは変わらず、Bitcoinの125倍のトランザクションスループットを達成する。したがって、Algorandの合意時間はブロックサイズとは無関係であり、大きなブロックに対してもほぼ同じ(平均12秒)にとどまることを示している。次世代のAlgorandでは、最終ステップをパイプライン処理することでスループットをさらに向上させることができると主張される(約6秒)。ビザンチン合意を実行するための固定時間と追加的なブロック伝搬時間の線形成長(ブロックのサイズを考慮)は、ブロックサイズを大きくすると、より多くのデータをコミットするのに要する時間を圧縮することができ、スループットを向上させることができる。

#  3.4  コスト 

Algorandを実行しているユーザーにはCPU、ネットワーク、およびストレージのコストが発生する。 CPUのコストはわずか。 VMごとに50人のユーザーを実行すると、8コアVMのCPU使用率は約40％(大半はデジタル署名とVRFを検証するために使用される)。つまり各Algorandプロセスではコアの約6.5％が使用される。帯域幅の観点から1Mバイトブロックと50,000ユーザーの実験では、各ユーザーは約10 Mbit / secを使用する。ユーザーあたりの通信コストはAlgorandを実行しているユーザーの数とは無関係である。これは、ユーザーがメッセージをゴシップする数が固定されているためだ。また、コンセンサスプロトコルのメッセージ数は(ユーザーの総数ではなく)委員会の参加ユーザー数に依存する。

ストレージコストの観点から、Algorandは、ブロックがコミットされたことを新規ユーザーに証明するためにブロック証明書を保管する。このストレージコストは、ブロック自体に追加されます。各ブロック証明書はブロックサイズに関係なく300 KBに上る。 1Mバイトのブロックの場合、これは最大30％のオーバーヘッド(間接費)となる。ユーザー間でのブロックストレージのシャーディング(独立したデータベース間でデータを水平にパーティション化すること)はコストを削減してくれる。たとえば、10を法とするシャーディングでは、各ユーザーは、元帳に追加される1MBブロックごとに平均して130 KBを格納する必要がある。ブロックの最大30％よりもコストが軽減されている。

# 4 未来の仕事

現状のAlgorandは合意プロトコルに集中されたもので、まだまだ実装のために必要な部分がある。この”Algorand: Scaling Byzantine Agreements for Cryptocurrencies”では、以下のことが「未来の仕事」として言及されている。

* インセンティブ。 ユーザがAlgorandに参加しネットワークコストを支払うにはインセンティブを含める必要があるかもしれず、報奨メカニズムが有望である。インセンティブメカニズムの設計と分析には多くの課題が含まれる。投票を保留するのようなひどいインセンティブや悪意のあるユーザーがプロトコルに従うユーザーよりも多くの報酬を得るために「システムを操作する」ことが例に挙げられる。
* 参加コストの低減。Algorandに参加するには新規ユーザーは付随する証明書を含むすべての既存のブロックをフェッチしないといけない。これは大量のデータの移送を意味する。 他の暗号化通貨も同様の問題に直面しているが、Algorandのスループットが比較的高いため、ブロックの連なり(ブロックチェーン)の総サイズが肥大し、ノード当たりのストレージコストを増やし、スケーラビリティ問題が発生する可能性がある。
* 攻撃者は、メッセージを送信した後に委員の身元が明らかになるため、時間の経過とともにユーザーに”汚職”を働く可能性がある。 攻撃者が十分なユーザーキーを取得できれば、フォークを生みだすための偽の証明書を作成できる。 1つの解決策は、署名されたメッセージを送信する前に署名鍵を消失させることだ。

同時に9月にミラノで開かれたミートアップでは、MicaliがAlgorandの将来について通貨、プラットフォーム、金融ツールの3つの可能性に言及している。短期的な目標として、モバイルペイメントへの応用やダッチオークションでトークンを売る可能性に触れている。長期的な目標として、スマートコントラクト、オンチェーン債権の開発に触れている。
￼
# 5. 評価1:改善されたPoS

AlgorandがPoSの発展にあたるとわかった。では両者はどう違うか。

最も優れているPoSと考えられているTendermint ConcensusとAlgorandを比較してみよう。Tendermint Concensusではあるノードがランダムに提案者に選出され新しいブロックを提案する。他の参加者が検証者になり一定の制限時間内に2/3以上の投票数が集まれば1段階目の投票プロセスで承認される。1段階目の投票プロセスを通過したブロックは2段階目の投票プロセスに送られる。今度は異なるノードが提案者に選出され、検証者の2/3以上が投票すれば正式にブロックが承認されたことになり、新しいブロックとしてブロックチェーンに追加される。

![consensus logic.e9f4ca6f](//images.ctfassets.net/4l4ail9691ba/5YZaFRAD04GMK2Am4YKaUu/67ca56eb87f70a78585849cd650f5ee1/consensus_logic.e9f4ca6f.jpg)
Fig04 concensus process of Tendermint via Tendermint

1人のバリデーターによって新しいブロックが提案され、他のバリデーターらによって一定の制限時間内に2/3以上の投票数が集まれば1段階目の投票で承認される。1段階目の投票プロセスを通過したブロックは2段階目の投票プロセスに送られ、ここでも2/3以上の投票数を得ることができれば正式にブロックが承認されたことになり、新しいブロックとしてチェーンに追加される。Tendermintでは他のPoSと同様もっているステークに応じて投票権が配分され、投票権の2/3のが善意の参加者であるという合意成立の条件があるのだ。2回投票を繰り返すのは、仮にビッグプレイヤーがいて合意を脅かすとしても、2度2/3の投票を乗り越えていれば確率的に偽りの承認ではないことが確かだからである。ブロックをゴシッププロトコルで伝播させ短い時間で承認か否かを決断させる点も似ている。

他にもPoSにはDelegated Proof of Stake(DPoS)という発展形がある。コインの保有者に保有量に応じた投票権を割り当て、その投票により取引の検証者を委任するアルゴリズムである。委任された検証者は、ブロック生成で得られた報酬を投票した人に還元する仕組みになっている。これはほぼ「代表民主制」に近似する仕組みである。DPoSは実践としては保有者がデフォルトで検証者の選出に賛成している仕組みであることが多い。なぜなら少量保有者には検証者の選出に投票に参加する誘因が弱い。面倒くさいことはしたくないだろう。だとしたら代表する検証者の善意を信じてお任せにできるなら嬉しい。そのため投票者を選ぶ投票はある意味、形骸化しており、余分なコストがかかっている。

Algorandは検証者の選定方法がTendermintやDPoSとも異なる。提案者と委員会のランダム選択、両者の匿名性(後に証明書付きで周知される)、検証の即時性で、低いコストでBFTを獲得していると考えられる。「提案、合意、確定」を繰り返すだけの仕組みにより、Bitcoinが背負うファイナリティ(settlement finality)の問題を背負うことがない。Bitcoinはフォークしうるためどの時点で取引が確定したかの線引きが確率的にしかできず、これが少額高頻度決済への応用の壁となる。従来型ブロックチェーンではブロックが提案された後、全員に配られそれぞれのチェーン固有のメカニズムによって合意されなければならなかったり、ブロックをファイナライズする前に追加作業が差し込まれたりする。これに対しAldorandは取引確定を決定論的に線が引けるとMicaliらは主張している。「ブロック承認時間が短く選出されたリーダーが正直である場合はたった2ステップで合意に達する、これは概ね従来型ブロックチェーンより簡潔である」と。Tendermintはビザンチン合意を満たすコンセンサスアルゴリズムとしてはかなり高いスループットを主張している。どちらが優れているか、すべてはAlgorandを実際に動かしてみればわかることだ。

# 5.1 ネットワークパーティション耐性

Bitcoinでは採掘者には新しいブロックを生成し配り、他の採掘者は個々に独立してそのブロックの妥当性を検証するプロセスを踏む。実はこのタイミングがあまりセキュアではないとセキュリティの専門家から指摘されている(セキュリティ屋さんの指摘は他にもたくさんある)。攻撃者はネットワークパーティション(ネットワーク内の同期が崩れてしまう状況)が起きた瞬間をつつけば、分離されたクラスタでプロトコルに則りながら偽りのブロックを生成し承認させられる可能性がある。Bitcoinはチェーンの分岐が起きた際には最も長いチェーンが支持され、分岐を解消する仕組みを採用している。だが、分岐をそのまま維持し、別のネットワークとして”独立”させてしまう手段があり、頻発してきた。

瞬間合意プロトコルはこの攻撃可能性を極小化できているだろうか。Argolandは「プロトコルは長さが不明な任意のネットワークパーティションに対して復元力があり、パーティションが解決され、遅延が復元された後、速く回復する」と説明している。 繰り返すが、正直なリーダーがトランザクションのブロックを提案すると、最初の投票ステップはブロックの伝搬と並行して行われる。ブロックが伝播した後、投票の1つのステップで証明書が生成される。これが簡潔かつ即時的なビザンチン合意プロセスの利点である。

# 6. 結論

Algorandのポイントは参加者の他者との情報隔離と秘匿性である。これでセキュリティをトレードオフにせずに即時的なトランザクションを可能にしている。ビザンチン合意を安く達成しているのなら、AlgorandはBitcoinの地位を奪う可能性が十分にあるだろう。Algorandが主張している性質をもつかいなかは保有者を増やせばわかる。Micaliはトークンセールをダッチオークションで行うと9月のミランでのミートアップで語っている。2/3の投票権が善意のプレイヤーのもとに渡るように慎重を期する必要がありそうだ。

Algorand論文は効率的なビザンチン合意アルゴリズムの導出に注力しているが誘因設計が残された最後の関門である。先行例のPoSは報酬設計がプレイヤーに「独占戦略」の誘因を生じさせた。最悪シナリオではプレイヤーがNemの例で指摘したようなモラルハザードを引き起こすことになる。一方投票に参加する利得を作らないことにはビザンチン合意が担保できないため、最後のもうひと知恵が必要な段階である。

最も有望な応用はやはり通貨である。Bitcoinよりも早く堅牢なビザンチン合意を達成する通貨があれば、Bitcoinが見た高コストの「信頼される第三者」を代替する夢を見ることになるだろう。プラットフォームとしてはEthereumがERC20トークン等の形態で提供するトークン発行機能が有望だと考えられる(関連記事[「Erc20トークンの可能性とそのネットワーク外部性」](https://axion.zone/entry/erc20token-and-network-externality/))。

Ethereum等にはブロックチェーンをアプリケーション構築の基盤と捉える向きがあるが、データベースでの合意を分散合意にする理由、しかも最も難易度の高い未知の多数によるビザンチン合意で達成する必要性はほとんど見つけることができない。GCP Cloud SpannerではPaxosが使われているが、これも既知の少数による悪意を想定しないもので分散合意のなかでもは難易度が低い。PoSという手段とアプリケーション基盤という目的がほとんどマッチしていないので、マーケティングされているDapps(分散アプリケーション)ではなく、AWS、GCP、Azureでのアプリケーション構築が推奨される。最後に金融ツールとしての応用があるが、債権の台帳とするのは素晴らしいアイデアのようにも感じられる。繰り返しになるが、誘因設計がどうなるかを見守る段階だ。プロトコルを堅牢にするための様々な仕掛けにはMicali先生の経験が生きているだろう。今後のインセンティブ設計とその安定的な運用については、最初の論文の共著者でHead of theory research and chief scientist のJing Chen氏のほか、アドバイザーに名を連ねるゲーム理論家、経済学者の力が試されている。

# 7. 感想

Micali先生はゼロ知識証明の発明者で、ゼロ知識暗号の新しい形式であるzk-SNARKs(Zero-Knowledge Succinct Non-Interactive Argument of Knowledge)はZcashという暗号通貨で最初に採用されている。用途はトランザクションの内容を知らずしてそのトランザクションの成否を承認するプロセスのためであり、Ethereumなどの他の通貨でもzk-SNARKsは採用されている。BitcoinはMicali先生の貢献分野がてんこ盛りであり、”血が騒いだ”というが今回の参入の背景だと勝手に推察する。

Algorandの論文読みは大変だったし、すべてを理解できたとはまったく思っていない。この挑戦は高度な学問領域の合わせ技なので、各領域の方からその説明は誤っていると言われるかもしれない。ご指摘をお待ちしています。

# Reference

ALGORAND AGREEMENT: Super Fast and Partition Resilient Byzantine Agreement
https://eprint.iacr.org/2018/377

Yossi Gilad, Rotem Hemo, Silvio Micali, Georgios Vlachos, Nickolai Zeldovich 
”Algorand: Scaling Byzantine Agreements for Cryptocurrencies”
https://dl.acm.org/citation.cfm?id=3132757

Jing Chen, Silvio Micali ”ALGORAND”
http://48d6hp28tnn92pdfye2fog4w-wpengine.netdna-ssl.com/wp-content/uploads/2018/10/Theoretical.pdf

Silvio Micali, Michael Rabin, Salil Vadhanz “Verifiable Random Functions”
https://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Pseudo%20Randomness/Verifiable_Random_Functions.pdf

Amy Castor, coindesk ”Scaling Consensus? This Turing Winner Thinks He’s Found a Way”
https://www.coindesk.com/scalable-blockchain-consensus-turing-award-winner-thinks-hes-got-solution

今度こそ絶対あなたに理解させるPaxos
https://qiita.com/kumagi/items/535c9b7a761d2ed52bc0