
## Önceden Kurulu driver ve cuda dosyaların kaldırılması kısmı. 
sudo apt-get purge nvidia*

sudo apt remove nvidia-*

sudo rm /etc/apt/sources.list.d/cuda*

sudo apt-get autoremove && sudo apt-get autoclean

sudo rm -rf /usr/local/cuda*


## Cuda grafik kartının kullanılabilir olduğu kontrol edilir.
lspci | grep -i nvidia

## İşletim siteminde gcc kurulur.
sudo apt-get install gcc

## Sistem update edilir.
sudo apt-get update

## Diğer gerekli paketler kurulur.
sudo apt-get install g++ freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev

## Kernel güncellenir.
sudo apt-get install dkms

## Nvidia PPA repo repo dosyası eklenir.
sudo add-apt-repository ppa:graphics-drivers/ppa

sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub

echo "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" | sudo tee /etc/apt/sources.list.d/cuda.list

## Download Klasörü içerisinde cuda install dosyası indirilir.
wget https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64

sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb

sudo apt-get update

sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb


## Cuda 10.0 kurulur.
sudo apt-get -o Dpkg::Options::="--force-overwrite" install cuda-10-0 cuda-drivers


## Cuda path dosyası eklenir.
echo 'export PATH=/usr/local/cuda-10.0/bin:$PATH' >> ~/.bashrc

echo 'export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc

source ~/.bashrc

sudo ldconfig

## Cudnn dosyası kururlur. Bu dosya indirilebilmesi için nvida'ya üye olmak gerekir. Aşağıdaki linkten üye olunabilir.
# https://developer.nvidia.com/developer-program/signup
# Bu sayfaya gidilir. https://developer.nvidia.com/cudnn
wget https://developer.nvidia.com/compute/machine-learning/cudnn/secure/7.6.5.32/Production/10.1_20191031/cudnn-10.1-linux-x64-v7.6.5.32.tgz

tar -xzvf cudnn-10.0-linux-x64-v7.6.5.32.tgz


## İndirilen dosyalar cuda toolkit dosyasına kopyalanır
sudo cp -P cuda/include/cudnn.h /usr/local/cuda-10.0/include

sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-10.0/lib64/

sudo chmod a+r /usr/local/cuda-10.0/lib64/libcudnn*

## Son olarak kurulum kontrol edilir.
nvidia-smi

nvcc -V


##Open Cv Kurulumu için 
tar -xzvf Install-OpenCV-master.zip

cd /Install-OpenCV-master/Ubuntu

##En son versiyon OpenCV kütüphanesi için aşağıdaki komut çalıştırılır.
./opencv_latest.sh 
