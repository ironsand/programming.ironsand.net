---
title: RubyとRasberry Pi でLEDをチカチカさせる
author: 鉄
type: post
date: 2015-02-22T12:14:42+00:00
url: /2015/rubyとrasberry-pi-でledをチカチカさせる/
categories:
  - Raspberry Pie

---
Rasberry Piに初期設定をして電源を挿すだけでノートパソコンから操作できるようにはしたももの、電子工作！！な事を全然やってないし、やり方もわからなかったのでAmazonでそれっぽいスターターキットを買ってみました。

<a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00G86DOP8/ironsand0b-22/ref=nosim/" rel="nofollow" ><img src="http://ecx.images-amazon.com/images/I/51LuR8kp9nL._SS500_.jpg" style="border: none;" alt="ハック ラズベリーパイ Raspberry Pi 電子工作入門キット。" /></a>

### 基礎知識

LEDから出てる日本の先端のうち長いのがアノード(電流が入ってくる方)、短いのがカソード(電流が出て行く方)。

GPIO(General-purpose input/output)のそれぞれのピンの役割は以下のとおり。単純に3.3Vや5Vの電圧のところもあるし、Ground(GND)、それにGPIOがある。

つまり全体のこともGTIOと呼ぶし、一部のその機能をもつピンもGPIOと呼ぶらしい。めんどくさい…。

[<img src="http://programming.ironsand.net/wp-content/uploads/2015/02/gpio-led.png" alt="gpio-led" width="564" height="424" class="alignnone size-full wp-image-602" srcset="http://programming.ironsand.net/wp-content/uploads/2015/02/gpio-led.png 564w, http://programming.ironsand.net/wp-content/uploads/2015/02/gpio-led-300x226.png 300w" sizes="(max-width: 564px) 100vw, 564px" />][1]

`B+`のモデルにはもっとピンがあるんですが、`1`から表示されてる部分までは同じらしいです。ちなみに後ろのハンダ付けが四角いのが`1`だそうです。……なにそのわかりにくい基準。

[<img src="http://programming.ironsand.net/wp-content/uploads/2015/02/backside_raspberrypi.jpg" alt="backside_raspberrypi" width="1352" height="800" class="alignnone size-full wp-image-609" srcset="http://programming.ironsand.net/wp-content/uploads/2015/02/backside_raspberrypi.jpg 1352w, http://programming.ironsand.net/wp-content/uploads/2015/02/backside_raspberrypi-300x178.jpg 300w, http://programming.ironsand.net/wp-content/uploads/2015/02/backside_raspberrypi-1024x606.jpg 1024w" sizes="(max-width: 1352px) 100vw, 1352px" />][2]

抵抗には向きはないが強さは線の色で決まるので覚えるのが大変。

ブレッドボードは基礎知識がないとつらいのでこちらを読んでおいてください。
  
<http://jsdiy.web.fc2.com/avr_7segclockbb/>

### LEDをチカチカさせる

最初に載せたキットの解説サイトが[こちら][3]ですので、そこを参照します。

### 配線方法

ブレッドボードの配線がこんなんで、

[<img src="http://programming.ironsand.net/wp-content/uploads/2015/02/codes_breadboard.jpg" alt="codes_breadboard" width="1067" height="800" class="alignnone size-full wp-image-605" srcset="http://programming.ironsand.net/wp-content/uploads/2015/02/codes_breadboard.jpg 1067w, http://programming.ironsand.net/wp-content/uploads/2015/02/codes_breadboard-300x225.jpg 300w, http://programming.ironsand.net/wp-content/uploads/2015/02/codes_breadboard-1024x768.jpg 1024w" sizes="(max-width: 1067px) 100vw, 1067px" />][4]

ラズパイの配線がこんなんで

[<img src="http://programming.ironsand.net/wp-content/uploads/2015/02/codes_raspberry.jpg" alt="codes_raspberry" width="1067" height="800" class="alignnone size-full wp-image-606" srcset="http://programming.ironsand.net/wp-content/uploads/2015/02/codes_raspberry.jpg 1067w, http://programming.ironsand.net/wp-content/uploads/2015/02/codes_raspberry-300x225.jpg 300w, http://programming.ironsand.net/wp-content/uploads/2015/02/codes_raspberry-1024x768.jpg 1024w" sizes="(max-width: 1067px) 100vw, 1067px" />][5]

コードがこうです。解説サイトのRubyを修正しています。

<pre class="lang:ruby decode:true " title="/home/pi/led_blink.rb" >port = 24
File.write("/sys/class/gpio/export", port)
sleep 0.2 # 書き込みエラー回避
File.write("/sys/class/gpio/gpio#{port}/direction", "out")

(1..10).each do |i|
  File.write("/sys/class/gpio/gpio#{port}/value", i % 2)
  sleep 0.2
end

File.write("/sys/class/gpio/unexport", port)</pre>

### Lチカさせる

以上が上手くいっていたら `ruby ~/led_blink.rb`でスクリプトを実行したらLEDがチカチカと5回点滅するはずです。やったー！！

できなかった人は一つ一つ手順を確認していきましょう〜。

それではみなさん楽しい Raspberry Pie 生活をお過ごしください。 ノシ

