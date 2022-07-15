# Japanese Movie Recommendation Dialogue #

### Overview ###
This is a Japanese knowledge-grounded dialogue dataset about the movie recommendation between humans.
Every recommender's utterance in dialogues is associated with the movie information as external knowledge.
The external knowledge used in this dataset is hierarchically structured into knowledge types common to all movies (e.g., "Title", "Released Year") and knowledge contents for each movie (e.g., "Rise of Planet of the Apes", "August 5, 2011").

This dataset consists of about 5,000 dialogues between crowdworkers, and each dialogue consists of 23 utterances on average.
Some dialogues contain the results of post-task questionnaires conducted with the dialogue participants.


### Files ###
The `data` directory contains the following files
- `{train/valid/test}.json`: All dialogues in this dataset divided into the train (4,575 dialogues), valid (200 dialogues), and test sets (300 dialogues).

Note that the number of dialogs and data splitting is different from the reference papers.

### Format ###
Each file has the following format.
```text
[
  {
    "dialog_id": "03042",
    "movie_title": "インディ・ジョーンズ／最後の聖戦",
    "first_speaker": "seeker",
    "questionnaire": {
      "recommender": {
        "Q1": 3,
        "Q2": 3,
        "Q3": 3,
        "Q4": 3,
        "Q5": -1
      },
      "seeker": {
        "Q1": 4,
        "Q2": 3,
        "Q3": 1,
        "Q4": -1,
        "Q5": 4
      }
    },
    "knowledge": {
      "[知識なし]": "[知識なし]",
      "タイトル": "インディ・ジョーンズ／最後の聖戦",
      "製作年度": "１９８９年",
      "監督名": "スティーヴン・スピルバーグ",
      "監督説明": "アメリカ合衆国の映画監督、映画プロデューサー",
      "キャスト名": [
        "ハリソン・フォード",
        "ショーン・コネリー"
      ],
      "キャスト説明": [
        "アメリカ合衆国出身の俳優。映画『スター・ウォーズ』シリーズ、『ブレードランナー』シリーズ、『ジャック・ライアン』シリーズなどの関連作品出演で知られ、特に代表作『インディ・ジョーンズ』シリーズでは、長きに渡り主演を務めた。",
        "スコットランド出身の元映画俳優。『００７』シリーズの初代ジェームズ・ボンド役で有名。"
      ],
      "ジャンル": [
        "アクション",
        "アドベンチャー"
      ],
      "レビュー": [
        "毎回出現するマドンナ。インディが誘惑されずに“秘宝”をゲットできるのか、ハラハラさせられる。",
        "インディ・ジョーンズシリーズの３作目で、今まで語られることのなかった、インディの少年時代も描かれている。",
        "毎回インディは秘宝を探しに危険を顧みず旅をする中で、父親も絡んでくるところが見もの。",
        "シリーズの中で一番面白いです。",
        "迫力のある冒険シーンが素晴らしい。手に汗を握ります。"
      ],
      "あらすじ": [
        "舞台は１９３８年。",
        "冒険家として、また考古学教授として多忙な日々を過ごすインディ・ジョーンズに、大富豪ドノバンから相談が持ちかけられる。",
        "イエス・キリストの聖杯の所在を示す重大な遺物を手に入れたが、調査隊の隊長が行方不明になり、それを探して欲しいというのだ。",
        "最初は渋っていたインディだったが、その行方不明になった隊長というのが自分の父、ヘンリー・ジョーンズであると聞き、仕方なく依頼を承諾。",
        "父が最後に消息を絶ったヴェネツィアに向かった。",
        "そこで父の同僚エルザ・シュナイダーと合流、教会の中で聖杯捜しの鍵となる石板を発見するが何者かに襲われる。",
        "襲ってきた男から父はブルンワルド城に閉じこめられていることを聞かされ、インディはシュナイダーと共に救出に向かう。",
        "幽閉された父との再会も束の間、シュナイダーの裏切りによりインディは親子共々捕まり、手帳も奪われてしまう。"
      ]
    },
    "dialog": [
      {
        "utterance_id": "03042_00",
        "speaker": "seeker",
        "text": "宜しくお願いします。"
      },
      {
        "utterance_id": "03042_01",
        "speaker": "recommender",
        "text": "お願いします。インディ・ジョーンズ／最後の聖戦を紹介します。",
        "checked_knowledge": [
          {
            "type": "タイトル",
            "content": "インディ・ジョーンズ／最後の聖戦"
          }
        ]
      },
      ...
    ]
  },
  ...
]
```

- `dialog_id`: unique dialogue ID.
- `movie_title`: movie title recommended in the dialogue.
- `first_speaker`: The first speaker of that dialogue. It is either `seeker` or `recommender`.
- `questionnaire`: The results of the post-task questionnaires for the recommender and the seeker. All questions are answered on a 5-point Likert scale, with five being the best and one being the worse. `-1` indicates a missing answer to that question.
  - `Q1`: Do you like movies?
  - `Q2`: Did you enjoy the dialogue?
  - `Q3`: Do you know the movie you recommended (or that was recommended to you)?
  - `Q4`: Do you think you have recommended the movie well?
  - `Q5`: Do you want to watch the recommended movie?
- `knowledge`: External knowledge used in the dialogue. Only the recommender has access to this knowledge. `[知識なし]` indicates a special option chosen when the recommender does not use any knowledge, such as greetings.
- `dialog`: The dialogues. Each dialogue is a list of utterances. Each utterance is a dictionary with the following keys:
  - `utterance_id`: unique utterance ID. The format is `<dialog_id>_<turns-of-dialogue>`.
  - `speaker`: The speaker of the utterance. It is either `seeker` or `recommender`.
  - `text`: The text of the utterance.
  - `checked_knowledge`: List of knowledge used in the utterance. This key exists when the `speaker` is the `recommender`. Each used knowledge is a dictionary containing the knowledge type and knowledge content.　The knowledge listed here is always included in `knowledge`.

### References ###
- 児玉貴志, 田中リベカ, 黒橋禎夫: 外部知識に基づく発話生成に向けた日本語映画推薦対話データセットの構築, 言語処理学会第27回年次大会 (NLP 2021), 北九州, 2021. https://www.anlp.jp/proceedings/annual_meeting/2021/pdf_dir/B5-3.pdf
- Takashi Kodama, Ribeka Tanaka, and Sadao Kurohashi: Construction of Hierarchical Structured Knowledge-based Recommendation Dialogue Dataset and Dialogue System, In Proceedings of the The 2nd DialDoc Workshop on Document-grounded Dialogue and Conversational Question Answering, Dublin, Ireland / Online, 2022. https://aclanthology.org/2022.dialdoc-1.9/

###  Acknowledgment ###
This construction of this dataset was supported by NII CRIS collaborative research program operated by NII CRIS and LINE Corporation. This work was also supported by JST, CREST Grant Number JPMJCR20D2, Japan.

### License ###
CC-BY-SA 4.0
