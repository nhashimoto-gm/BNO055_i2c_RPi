# BNO055_i2c_RPi

https://github.com/nhashimoto-gm/BNO055_i2c_RPi

## 使用センサー
Bosch Sensortec GmbH Smart sensor: BNO055

( https://www.bosch-sensortec.com/products/smart-sensors/bno055/ )

Adafruit BNO055 Absolute Orientation Sensor

( https://learn.adafruit.com/adafruit-bno055-absolute-orientation-sensor )

## 接続機器と接続方法
RaspberryPIにi2c接続で通信。

以下の通信速度で使用したほうがデータ取得安定します。

標準のbaudrate=100000では、" OSError: [Errno 121] Remote I/O error " が頻発しました。

- dtparam=i2c_arm_baudrate=50000

(留意点) プルアップ抵抗は不要です。

(留意点) OSErrorは受け流すことにしました。

## 注意
LOCAL NETWORK上のInfluxdb v1.8サーバーへデータを送信。

InfluxQLは以下のような形で情報取得。(Grafana等利用)
```
SELECT mean("eu_x-axis") FROM "bno055_measure_euler" WHERE $timeFilter GROUP BY time($__interval) fill(none)
```

## Acknowledgments ( 謝辞 )

ghirlekar, you have been very helpful.

https://github.com/ghirlekar/bno055-python-i2c
