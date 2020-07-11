こんにちは。赤羽です。同日に２つも質問を出してしまい申し訳ありません。
## 1 小課題の選択された学校のurlへとべるようにする。
ヒントにLaunchyを使用してみましょうとあったので、選択する、ある工程を入力したら終了するようwhile文を使用すれば良いのかと思い、以下のようにコードを記述しました。
<details>
<summary>コード</summary>

```

class School
  attr_accessor :name,
                :address,
                :number_of_students,
                :founding_years,
                :introduction_video_url,
                :introduction_statement
  # 属性の宣言を、複数行う場合はカンマで区切る
  def initialize(name, address, number_of_students,founding_years,
                 introduction_video_url, introduction_statement)
    @name = name
    @address = address
    @number_of_students = number_of_students
    @founding_years = founding_years
    @introduction_video_url = introduction_video_url
    @introduction_statement = introduction_statement
  end
  def sample_instance_method
    puts("#{@name}は#{@address}にあリます。")
    puts("#{@number_of_students}人の生徒がいて,創立してから#{@founding_years}年経ちました。")
    puts("#{@introduction_statement}と言う特徴があります。")
  end
  def sample_school_hp
    require 'Launchy'
    while true
      puts "1〜３を選んでください"
      puts "1: A学校のサイトにアクセス"
      puts "2: B学校のサイトにアクセス"
      puts "3: どちらもみない"

      choice = gets.to_i

      if choice == 1
        puts(Lanchy.open("a_school@introduction_video_url"))
      elsif choice == 2
        puts(Lanchy.open("b_school@introduction_video_url"))
      elsif choice == 3
        puts "終了します"
        break
      else
        puts "1~3 の数字を入力してください。"
      end
    end
  end
end
# インスタンスの作成
a_school = School.new("A学校", "東京都渋谷区..", 300, 100, "https://hoge.com", "A学校は自然豊かな...")
a_school.sample_instance_method
a_school.sample_school_hp
b_school = School.new("B学校", "東京都新宿区..", 500, 30, "https://foo.com", "B学校は文武両立で...")
b_school.sample_instance_method
b_school.sample_school_hp
# インスタンスメソッドは、インスタンス変数を呼び出す時と同様にインスタンス.インスタンスメソッドとして呼び出せる


```

</details>

### 2エラーについて
しかし実際に実行しようとすると、入力までは上手くいくのですが`uninitialized constant Lanchy (NameError)
Did you mean?  Launchy`とエラーが出てしまいます。
エラーを調べてみたところクラスが読み込めていないと言うものが出てきました。

### 3行ってみたこと
①`require`が上手く動いていないのかなと思い、classを定義する前に置いてみたりもしたのですが、特にエラーが変わりませんでした。
②`@introduction_video_url`の表現がダメなのかと思い、urlをそのまま記述してみたりもしたのですがエラーが変わりませんでした。
③sample_school_hpメソッドで定義するのではなく、Schoolクラスの外？で記述もしてみたのですが同様のエラーでした。
どこの部分の記述を直せばとぶのかがさっぱりわかりません…。ちなみに３を選択すると正常にループは終了します。
ご助言お願いします。
