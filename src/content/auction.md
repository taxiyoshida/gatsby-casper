---
title: "Googleの検索広告で学ぶオークションの理論と実践"
author: Ghost
tags: ["Getting Started"]
image: img/murakami.jpg
date: "1922-12-12T10:00:00.000Z"
draft: false
---

以前、アドテクの歴史と背景についての記事を書いたら、とある界隈ととある界隈のふたつから熱烈な反響があった。僕は味をしめた。時間を見つけてもう一つ書いてみることにした。デジタル広告は巨大産業だが、バズワードである”アドテク”の旬は完全に終わっている。市場はGoogle、Facebook、Amazon、その他大勢に集約されつつある。フロンティアである中国、インド、東南アジアのデジタルエコノミーでは、デジタル広告は富裕国ほど重要性を表現しない。広告単価が安すぎたり、彼らはコンテンツに直接 / 間接的にお金を払ったりするのだ。

ぼくは自分の再学習も兼ねてこのブログを書いており、旬の過ぎたアドテクにだけフォーカスするのは自分の得にならない気がする。日本特有の状況に踏み込むとどこからともなく矢文が飛んでくるかもしれないし、また病気で4ヶ月寝込むかもしれない(笑)。むしろ、アドテクの興味深い部分を抽出し、そこから学びを提供する記事にしようと考えている。

今回はデジタル広告取引の主要な方法である「オークション」を題材にする。オークションは”マーケットデザイン”という経済学の新しい研究領域に含まれ、GAFAのビジネスとも大きくオーバーラップする。だからこの文章はお金や出世、成功、恋愛、友情、努力、勝利が好きで仕方がないあなたのためになるだろう。この記事では、デジタル広告に関連するビジネスパーソンとエンジニアにデジタル広告オークションの理論と実践にまたがる地図を提供することを目的としている。”説明”に変なところがあれば突っ込んでもらいたいばかりである。

---

今回はGoogleの検索広告オークションを例に使おう。広告テクノロジー(アドテク)は鉄鋼産業と比べてとてもダイナミックな業界である。だからこそ”枯れている”検索広告は格好の題材であるし、それに関する論文も書籍もたくさん出版されている。Googleはオークションを通じて広告主に検索結果の上と横の広告スペースを販売している。この検索広告の背後では複雑なオークションが行われている。

検索広告の販売方法は、当初はインプレッション(表示数)あたりの固定課金でされていた。キーワードや販売額については、営業マンと広告主が交渉して決めていた。GoTo.comが草分け的な存在であり、後にOvertureと改名した後、Yahoo!がMicrosoftとGoogleとの競争環境の中で16億ドルで[買収](http://articles.latimes.com/2003/jul/15/business/fi-yahoo15)した。

Overtureは当時は最も成功した検索広告モデルだったが、完璧ではなかった。Overtureの販売方法には広告業界の”慣習”である「バーター」(この奇妙な業界用語の代わりがみつからなかった)が含みにされており、検索広告を多く買う広告主はオーガニックの検索順位を上げることが約束されていたという。つまり、お金を払えば検索順位自体を”買う”ことがある程度はできた。これに対し、競合のGoogleは個々に自動化されたオークションを導入し、課金方法をクリックあたりの課金と設定した。そのオークションはセカンドプライス(2位価格方式)オークションを採用している。Googleはノーベル経済学賞を受賞した米国の経済学者ウィリアム・ヴィックリーの知見を活用した。

# ダッチ, イングリッシュ, 1位, 2位

すべての入札が公表されるタイプのオークションは、公開入札オークション(open auction)と呼ばれる。公開入札オークションには競り上げ式(イングリッシュ[英国式])オークションと競り下げ式(ダッチ［オランダ式］)オークションの2種類がある。競り上げ式では最低落札価格から徐々に価格を上げ「それ以上の価格では買わない」というところで買い手は競りから降りる。最後に残った1人が勝者になる。一方競り下げ式は、高すぎると思えるような価格からスタートして「買った」という買い手が出てくるまで徐々に価格を下げていく。最初に「買った」と言った買い手が勝者となる。

公開入札オークションは頻繁に使用されるが、Googleやその他の検索広告はこれを使用していない。彼らはオークションを公開の場ではなく非公開の場で行う封印入札オークション(sealed-bid auction)を採用している。落札価格の種類は封印入札オークションの種類により異なる。

* 1位価格オークションでは、落札者は入札金額の最高額(つまり落札者が提示した金額)を支払う。
* 2位価格オークションでは、落札者は2番目に高い入札額を支払う。

公開オークションには競り上げと競り下げ、封印方式には1位価格と2位価格の計4通りがあるということだ。

# 異なるしかけで同じ収入

ヴィックリーは(1)2位価格方式と競り上げ式の売り手が戦略的に同じであり、あるいは(2)1位価格方式と競り下げ方式の売り手の期待収入が戦略的に同じであると主張した。これを収入同値定理と呼ぶ。収入同値定理を大幅に一般化したのは同じくノーベル経済学賞を受賞したロジャー・マイヤーソンである。収入同値定理は一定の仮定を織り込んでいる。すべての入札参加者が共通した価値算定体系から互いに独立した私的価値をもつとの仮定である。言い換えれば、個々の入札者が財に対する自分自身の評価額しか知らず、他の入札者の評価額は確率的にしか分からない、という不完全情報(incomplete information)の要素を織り込んだゲーム理論モデルから導かれる。その私的価値は強く落札と入札者の期待利得に影響するということだ。商品が最も高い私的価値をもつ入札参加者に配分され、最も低い私的価値をつけた入札参加者の得る期待利得はゼロとなる。

(1)2位価格封印入札と競り上げオークションが同値だというのは直感に反するかもしれない。だが、ある美術品を僕が10億円の価値があると私的価値を定め、ライバルは9億円だと思っている。他の参加者はもっと低い価値を算定しているとする。ササビーズのオークションなら、入札者が値を競り上げていき8億円台の後半で、ライバル以外の競争相手はオークションから降りてしまうはずだ。ライバルは9億円で声をかける。このとき、自分は10億、と正直に言う必要はない。相手より少しでも高い、9億1000万円の値を出せば、もうライバルには勝てる。だから、競り上げ式競売では参加者の中の第2位価格が、事実上の落札価格になる。

(2)の場合も言わばこの反対だ。競り下げは最初の一声で落札するため、他者の入札額に影響されず自身の入札額がそのまま落札額になる。競り負けたときの利得はゼロである。封印式で最も高い価格をつけることもまた、他者の入札情報とは関係なく入札額を設定する。ことのきも競り負けたときの利得はゼロである。ざっと状況を描写しただけだが、この2つのオークションが戦略的に同値なのが推し量れるのではないか。

収入同値定理は、一定の仮定のもとで、売り手の得る期待収入がオークション方式に依存しないことを示している。また、この仮定のもとでは、最も高い私的価値をもつ入札参加者が財を落札するので、最も欲しいと考える人に財が配分される意味合いでの効率性が満たされている。

# 勝者の呪い

国債、電波、公共事業のような財の価値がすべての参加者について等しい”共通価値財”の場合、概ね収入同値定理は働かない。最も重要なシグナルを受け取っていない参加者も、オークションの過程で共通価値が高いことを学習できるため、落札価格は高くなりやすい。例えば、金融機関は概ね同様の国債の価値算定を行い国債オークションに入札する。国債発行者(国)の情報を他者よりも緻密に分析している金融機関が連続して国債を落札しているという事実が、他の金融機関のポジションに影響し、落札価格が上昇するということがあるかもしれない。わかりやすく言うと「あいつは何か知ってそうだな。なるほどそういうことか」という推測が働いて情報の偏りがすぐに平らになりやすいオークションである。

このような共通価値財取引では、勝者の呪い(winner’s curse)という問題が生じることが指摘されている。勝者の呪いとは、落札者の提示した価格が全員の中の最高価格であるために、落札者が実際の共通価値よりも高い価格を支払い損をしてしまうことだ。ノーベル経済学賞を受賞した経済学者リチャード・セイラーが原油採掘権、オリンピック放映権、野球のフリー・エージェント選手獲得、企業買収等で指摘したのが最初である。

公共事業の入札はわかりやすい例だろう。建設会社は事業の概要を見れば、公共事業のコストを推定できる。そこにどれだけの利益を載せた入札額をひねり出すかが勝敗の分け目だが、公共事業が削減される昨今、建設会社はどうしても受注したいが余り、コストを割る価格で入札し受注してしまう。入札には勝ったが損をしてしまったわけである。

オークション理論で考えるオークションメカニズムは個人合理性(Individual Rationality)を想定している。オークションの入札者の目標は利得(Payoff)を最大にすることだ。利得とは入札者が受け取る純利益のことであり、入札者が商品を獲得した場合には商品への評価額と支払った価格の差となる。落札できない場合はゼロだ。だから合理的な経済人をアクターと想定したときには「勝者の呪い」は入札者にとって避けるべき事象である。しかし、ヒトは必ずしも合理的に行動しない、ということを証明し続ける経済学者がいる。リチャード・セイラーもその一人である。行動経済学の観点からの分析はとても興味深いが、ここでは後回しにする。

# 1位価格方式の失敗

Googleの検索広告に戻ってこよう。まずはなぜ1位価格ではなく2位価格を採用したか。それは1位価格の採用には問題が想定された。広告主に対して、他の入札者の入札額を情報とし入札戦略を逐次変更するインセンティブが働いてしまう。このインセンティブのせいで広告主はオークションの情報をモニターするコストを負担するはめになる。最悪シナリオでは価格が増えたり減ったりと波打つ価格サイクルが生じてしまうかもしれない。1位価格を採用すると、入札者のコストが増大し、非効率的である。広告商品としても広告主の「手離れ」が悪いので、予算支出先の優先順位が下がりうる。

他方、2位価格では、入札者は他の入札者の戦略に影響を受けない最適戦略が存在するとヴィックリーは主張している(「支配戦略」という)。入札者は”私的価値”一度戦略を定めてしまえばそれを維持するのが好ましく、参加者が同様の最適戦略を維持している限りは、他の外部要因の影響はあるにしても、入札額が安定する。広告主としても一貫した入札戦略を採用すればいいので、”手離れ”がいい。

支配戦略はシンプルだ。2位価格オークションでは入札者は商品の私的な評価額をそのまま入札額に設定すべきだ。封印オークションでは、入札者は他者の入札額や落札額という情報を知りえない。それぞれの入札者は独立して自己の利得を最大化するには評価額と同額で入札する。その価格で落札した際には評価額よりも低い価格が落札額になるため利得はマイナスに振れない地点で均衡する、という考えが背後にある。

2位価格オークションには「ヴィックリー・メカニズム」と呼ばれるしかけが働いている。「ヴィックリー・メカニズム」と呼ぶ。公共財供給における「クラーク＝グローブス・メカニズム」と合わせてVCG(ヴィックリークラーク＝グローブス)メカニズムと呼ぶ。

VCGメカニズムのもとでは「パレート効率性」が担保される。パレート効率性とは全員が自発的に正直に行動する結果、社会的に望ましい結果が得られる＝社会的余剰が最大化されることだ。同時に「インセンティブ両立性」も所与の要件として担保される。インセンティブ両立性(Incentive compatibility)とは、グループ全体の利益になる選択を保証するため、プレイヤーが偽りの申告をしても利得を得られないようにし、正直に行動することを推奨するメカニズムのことである。このパレート効率性とインセンティブ両立性が表現するのは、「皆が正直にやっていると社会的な利益が最も大きく、偽ることで利得が得ようとする個人的合理主義的な反応には、偽ることの利得をゼロにすることで対応する。正直にやるとうまくいくように設計され、そのしかけをクラックする術を奪ってもいるプレイヤーは正直に行動する」ということだ。

VCGメカニズムはすべての入札参加者が共通した価値算定体系から互いに独立した私的価値をもつこと、個人が合理的に行動するという仮定に支えられている。一方「勝者の呪い」が起きる、皆がその価値を共通して算定できる”共通価値”の存在する共通価値財では働かない。

かくしてVCGメカニズムは効率性と耐戦略性を兼ね備えていると想定できる。

# VCGメカニズムの実験

このVCGメカニズムの理論的な美しさの”自然実験”ともいうべきものがGoogle Ads(2018年にGoogle AdWordsから改名)の検索広告である。Googleはヴィックリーらの2位価格の知見を発展的に応用した。Googleが採用した2位価格オークションは「一般化2位価格オークション(GSP)」という種類である。普通の2位価格式とは相違点がある。詳細はこの通りである。Googleで一度検索ワードを入れてみる方が理解が早いかもしれない。

* 広告主による入札：各購入者は、一回のクリックでGoogleに支払う金額である入札額を送信する。
* Googleによるマッチング：広告スペースは購入者の入札単価の高い順に割り当てられる。したがって、最高入札者は最初の広告スペースを獲得し、2番目に高い広告スペースは2番目の入札者が獲得する。
* 広告主からGoogleへの支払い：各購入者はそのスペースに対して支払う価格は、一般化2位価格オークションの方法に従う。最高位の入札者は、第2位の入札者が第1のスペースに対して支払うべき価格を、第2位の入札者は第3位の入札者が第2のスペースに対して支払うべき価格を支払う。
* 入札額×クリック率(CTR)の高い順に広告が表示される。事前にどの位置に表示されるかはわからない。
* 広告は成果報酬型で、広告がクリックされたときに払う
* オークションは頻繁に開催される

Googleはこの方法で関連するいくつかのキーワードに対して検索結果ページにどの順番で広告が表示されるかを定めている。それが同時にGoogleの利得を最大化するようになっている。Googleはクエリと検索結果の関連性を高めるために検索システムを改善しており、検索広告のCTRの改善を継続している。Googleは四半期ごとにCTRを公表しているが、CTRはほぼ一貫して改善している(この改善こそ彼らの誇りなのかもしれない)。

# 課題と制約

オークション理論の実践である検索広告オークションにおける課題や制約を整理してみよう。

VCGメカニズムに大きく影響しそうなのもののひとつが、入札者が持つ予算制約である。インセンティブ両立性とパレート最適を維持したまま予算制約の影響を無化する手段が検討されている。この予算制約の問題は、実現可能な割り当てのシークエンス群に対して複数のキーワードと複数のスロットという複雑な組合せを持ちうる制約が存在する場合にはさらに困難になる、と考えられる。

プレイヤーの行動の非合理性も想定できる(先に触れた行動経済学がそれを示している)。偽りの入札額を提示しても利得がなく、ときに損をするとしてもその行動を一貫してとるプレイヤーなどさまざまな種類の非合理行動が想定できる。

オークショナーの不正への脆弱性もある。検索広告オークションでは、Googleを信頼することが義務付けられている。2位価格オークションでは、入札者は他者の入札情報を知りえず、オークショナーのみが知る不完全情報のモデルを採用しているため、Googleには落札者に虚偽の2位入札額を教えることで、本来よりも高い落札額を引き出す潜在的な”力”がある。封印入札では、入札者たちはお互いがいくらで入札したかを知る余地がない。仮に1万ドルで落札した商品のセカンドプライスが9999ドルだったとGoogleが主張したとき、入札者はGoogleが自分に提示されている2位価格について疑念をもつことになるだろう。オークショナーは入札価格の情報を改ざんする。

Googleの支配的な立場は収入最大化オークションのインセンティブがある。Googleは売り手とオークショナーの立場を兼ねている。つまり、胴元と2つのプレイヤーのポジションのうちのひとつを占めている。同時にGoogle検索はその存在が認められない中華圏以外では市場を支配している。可能性への言及に過ぎないが、Googleは通常のビジネスのロジックでいくと、売り手の収入が最大化されるオークションを作りたくなる。胴元と売り手を兼ねるGoogleにはそれが可能である。だが、収入最大化を図りすぎると、買い手を逃がすことになる。客は客で細やかな戦略をもっているので、その全てに対応するのはむずかしい。あるいは、収入最大化のため入札額を多く積んだ人が勝つ仕組みをつくると、それがユーザーが関連性のないリンクを見せられ、検索へのエンゲージメントを落とすという外部性を生み出す。Googleは長期的には損失を負いかねない。

入札者側にも、2位価格オークションをクラックする術がある。ひとつが共謀である。入札参加者の間で共謀（collusion）が結ばれると、売り手の得る収入が極端に低下する可能性がある。2位価格方式の方が1位価格方式よりも共謀にさらされやすい。2位価格の場合、ただ1人が十分に高い価格を提示し、残りの参加者がゼロの価格を提示するような共謀を結ぶと、その1人はタダで財を得ることができる。しかも、共謀に参加していない他の参加者がその財を獲得するには、とても高い価格を支払わなければならないため、共謀の事実を知っている場合には、どの参加者にとってもその戦略から外れるインセンティブが存在しない。共謀に参加するほうが合理的なので、共謀が生まれ維持されやすいだろう。

共謀を企図する参加者は、自分が入札したキーワードで検索をし、他の入札者の存在を確認する。Googleに関知されない形で連絡を取り合うことは容易である。

もうひとつは偽名入札である。入札者が複数の識別子で複数の入札を提出することは容易だ(例えば、複数の電子メールアドレスを利用して複数アカウントを保持する)。 1つの商品のみが販売されている場合、入札者は追加の複数の入札を使用して利益を得ることが難しい。しかし、インターネット広告のオークションでは、複数の商品が競られている。架空の名前で複数の入札を同時に提出すると、GVAの初期のプロトコルは耐性がなかった。

# 想定されるGoogle側の対応

これらに対してGoogleが行っていることを検討しよう。

* 入札者の行動に制約を与える。利用者は自動入札機能を使うことで、広告出稿に伴うコストを削減できるとともにパフォーマンスの最適化をできると宣言する。Googleは入札戦略ツール、入札単価調整アルゴリズムを入札者に渡している。利用者にはこの機能、ツールを使うインセンティブが働く。Googleは入札者は検索広告の設定時に広告予算の入力を求めている。一日あたりの広告費の制約を設けられるようにもしている。機能は入札行動を合理的にしVCGメカニズムの範疇に入れる。Googleは参加者の予算という制約を織り込んだアルゴリズムを導出しているはずだ。
* 共謀や偽名入札を検出するアルゴリズムを用意していると考えられる。
ダッシュボードから入札する限りは共謀を思いつかないようなインターフェイス設計である。合理的個人であることが奨励されている。

Googleはメカニズムデザイン上正しいことをしているかもしれない。ただしメカニズムの中で圧倒的に強力で信用せざるを得ない”Trusted First Party”である。この点はメカニズムの実践の成功要因であると同時に大きな脆弱性でもある。まさしく”Don’t be evil”である。

# Reference

Strategic Bidder Behavior in Sponsored Search Auctions
https://www.sciencedirect.com/science/article/pii/S0167923606001242

オークションの理論と実践2017
https://www.slideshare.net/mobile/YosukeYasuda1/2017-71399709

Richard H. Thaler “The winner's curse: paradoxes and anomalies of economic life”
https://press.princeton.edu/titles/5451.html

セイラー教授の行動経済学入門 https://www.amazon.co.jp/%E3%82%BB%E3%82%A4%E3%83%A9%E3%83%BC%E6%95%99%E6%8E%88%E3%81%AE%E8%A1%8C%E5%8B%95%E7%B5%8C%E6%B8%88%E5%AD%A6%E5%85%A5%E9%96%80-%E3%83%AA%E3%83%81%E3%83%A3%E3%83%BC%E3%83%89%E3%83%BB%E3%82%BB%E3%82%A4%E3%83%A9%E3%83%BC/dp/4478002630

Introduction to Economic Analysis
v. 1.0
https://saylordotorg.github.io/text_introduction-to-economic-analysis/index.html

20.5 The Winner’s Curse and Linkage
https://saylordotorg.github.io/text_introduction-to-economic-analysis/s21-05-the-winner-s-curse-and-linkage.html

上田晃三『オークションの理論と実際：金融市場への応用』
http://www.imes.boj.or.jp/japanese/kinyu/2010/kk29-1-2.pdf

MAKOTO YOKOO "False-name Bids in Combinatorial Auctions"
https://sigecom.org/exchanges/volume_7/1/yokoo.pdf

Image via Paul Hudson (flickr /  CC BY 2.0) / Takashi Murakami's Piece

