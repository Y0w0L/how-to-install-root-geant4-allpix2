# wsl2 Ubuntu20.04LTSにおけるLinux環境の構築についてまとめる  
usernameと書かれたところは自分のLinuxの名前に個人で変更  
まだ未完成　今後完成させるかも
## 作りたい環境  
windows11  
wsl2  
Ubuntu20.04LTS  
ROOT  
Geant4  
Allpix squared  
CUDA（できたら）  
※Allpix2がいらない場合はコンパイルのオプションが少し変わる。別にそのままでも使用可能  

## wsl2 Ubuntu20.04まで   
```wsl --install```  
正しいか分からない　覚えていないUbuntu20.04を入れる  
間違えたら以下のコマンドを入れる  
wsl --list  
wsl --unregister Ubuntu-????  
ちなみにwslから抜けたいときはexit  
シャットダウンしたいときはwsl --shutdown  
Linux環境ごとにシャットダウンするコマンドもネットに調べたらある  

## 必要なパッケージをダウンロードする  
足りないのがあった時はエラー文から適宜ダウンロード  
```sudo apt update```  
```sudo apt upgrade``` 　　  
```sudo apt install build-essential```    
```sudo apt qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools```    
```sudo apt install xerces-c-dev```    
```sudo apt install python3```    
```sudo apt install python3-pip3```    
※パッケージのダウンロードにおいてファイルを多すぎてエラーが出ることがあるが同じコマンドを打つとインストールできることがある  
python3についての設定  
```cd```  
```vi .bashrc```  
.bashrcの最後に  
```alias python="python3"```  
alias pip="pip3" <-いらないかも  
```bash```  

## 　ROOTをコンパイルする  
```cd```  
```mkdir root```  
```cd root```  
```mkdir install build```  
```git clone https://github.com/root-project/root.git root_src```  
```cd build```  
```cmake -DCMAKE_INSTALL_PREFIX=../install -DCMAKE_CXX_STANDARD=17 ../root_src```  
```sudo make -j10```  
```sudo make install```  
```cd```  
```vi .bashrc```  
末尾に以下の文を追加して保存  
```source /home/username/root/install/bin/thisroot.sh```  
```bash```  
```root```  
コマンドを打ってrootが起動したらok  
## Geant4をコンパイルする  
```cd```  
```mkdir geant4```  
```cd geant4```  
```wget https://geant4-data.web.cern.ch/releases/geant4-v11.1.2.tar.gz```  
```tar -xvf geant4-v11.1.2.tar.gz```  
```mkdir install build```  
```cd build```  
```cmake -DCMAKE_INSTALL_PREFIX=../install -DGEANT4_INSTALL_DATA=ON -DGEANT4_USE_GDML=ON -DGEANT4_USE_QT=ON -DGEANT4_USE_XM=ON -DGEANT4_USE_OPENGL_X11=ON -DCMAKE_CXX_STANDARD=17 -DGEANT4_BUILD_MULTITHREADED=ON -DGEANT4_BUILD_BUILTIN_BACKTRACE=OFF ../geant4-v11.1.2```  
```sudo make -j10```  
```sudo make install```  
```cd```  
```vi .bashrc```  
.bashrcの末尾に以下の文を加えて保存  
```source /home/username/geant4/install/bin/geant4.sh```  
使えるかどうかはネットでしらべてexampleをうごかしてみればよい  

## ここから下はAllpix2がいる人だけ　　
### eigen3 boostをダウンロードする　　

cd　　

