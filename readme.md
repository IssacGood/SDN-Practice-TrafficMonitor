# 測試環境:ubuntu 16.04 LTS
### 簡單安裝教學(https://github.com/playerlove1/SDN-test)

### 1.撰寫監控程式碼(simple_monitor.py)
#### 如圖
![](img/Code1.jpg)
#### 接續
![](img/Code2.jpg)

### 2.建置Mininet(in terminal)
 交換器1台(single)、host3台的拓璞(3)、使用Open vSwitch(ovsk)、指定外部的 OpenFlow Controller(remote)、啟動 xterm(-x)
```console
sudo mn --topo single,3 --mac --switch ovsk --controller remote -x
```
#### 如圖
![](img/sudomn.jpg)

### 3.查看Switch狀態(in s1-xterm)
 查看界面卡連接狀態
```console
ovs-vsctl show
```
#### 如圖
![](img/ovsvsctlshow.jpg)
### 查看介面卡與port連接狀態
```console
ovs-vsctl show
```
#### 如圖
![](img/ovsdpctl.jpg)

### 4.設定OpenFlow的版本為1.3(in s1-xterm)
```console
ovs-vsctl set Bridge s1 protocols=OpenFlow13
```
#### 如圖
![](img/setBridge.jpg)

### 5.檢查空白的Flow Table(in s1-xterm)
 ovs-ofctl用來指定OpenFlow版本。預設值是OpenFlow10
```console
ovs-ofctl -O OpenFlow13 dump-flows s1
```
#### 如圖
![](img/dumpflows1.jpg)

### 6.執行監控程式(in c0-xterm)
 --verbose列出詳細執行訊息、./當前目錄下的檔案
```console
ryu-manager --verbose ./simple_monitor.py
```
#### 如圖
![](img/ryuverbosesimplemonitor.jpg)

### 7.h1 ping h2(in h1-xterm)
 -c1代表ping一個packet、10.0.0.2 是 h2 ip
```console
ping -c1 10.0.0.2
```
#### 如圖
![](img/h1pingh2.jpg)

### 8.查看controller變化(in c0-xterm)
#### 如圖
![](img/c1whenh1pingh2.jpg)

### 9.比較前後差別(in c0-xterm)
#### 如圖
![](img/compare.jpg)




參考資料來源(https://osrg.github.io/ryu-book/zh_tw/Ryubook.pdf)