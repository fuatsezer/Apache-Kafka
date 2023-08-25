# Apache Kafka Kurulumu
Kafkayı Oracle Linuxe kurulumu aşağıda anlatılmaktadır
## Java Kurulumu
Kafkayı kurmadan önce javayı kurmalıyız
Javayı Oracle Linux makineye kurmak için aşağıdaki komutu kullanın
```console
[fuatsezer@localhost ~]$ sudo yum install java-1.8.0-openjdk.x86_64
```
Doğru kurulduğunu kontrol etmek için aşağıdaki komutu çalıştırın
```console
[fuatsezer@localhost ~]$ java -version
```
Aşağıdaki gibi bir çıktı vermeli.
```
openjdk version "1.8.0_382"
OpenJDK Runtime Environment (build 1.8.0_382-b05)
OpenJDK 64-Bit Server VM (build 25.382-b05, mixed mode)
```
 JAVA_HOME ve JRE_HOME ortam değişkenlerini tanımlayalım.
```console
[fuatsezer@localhost ~]$ export JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk
[fuatsezer@localhost ~]$ export JRE_HOME=/usr/lib/jvm/jre
[fuatsezer@localhost ~]$ source /etc/profile
```
Ortam değişkenlerinin Doğru tanımlandığını kontrol edelim.
```console
[fuatsezer@localhost ~]$ env | grep jre
```
Eğer ortam değişkenleri doğru tanımlandıysa aşağıdaki gibi bir çıktı almalısınız
![image](https://github.com/fuatsezer/Apache-Kafka/assets/63423939/7062f5d3-ad82-4aac-ab84-5a1d500761d8)

## Zookeeper ve Kafkayı Yükleme
Kurulum için aşağıdaki komutları çalıştırın
```console
[fuatsezer@localhost ~]$ cd /tmp/
[fuatsezer@localhost tmp]$ wget https://downloads.apache.org/kafka/3.5.1/kafka_2.13-3.5.1.tgz
[fuatsezer@localhost tmp]$ tar -xzvf kafka_2.13-3.5.1.tgz
[fuatsezer@localhost tmp]$ sudo mkdir /opt/kafka
[fuatsezer@localhost tmp]$ cd kafka_2.13-3.5.1/
[fuatsezer@localhost kafka_2.13-3.5.1]$ sudo cp -r * /opt/kafka/
[fuatsezer@localhost kafka_2.13-3.5.1]$ ls -la /opt//kafka/
```
Son komut aşağıdaki gibi bir çıktı vermeli
![image](https://github.com/fuatsezer/Apache-Kafka/assets/63423939/0cc2e1cc-9d6a-42c6-8e8e-7c5e0de92800)

## Zookeper ve Kafka servislerini Başlatma
İlk önce kafkanın meta verilerini saklayan zookeeper'ı başlatmalısınız aşağıdaki komut ile
```console
[fuatsezer@localhost kafka_2.13-3.5.1]$ cd /opt/kafka/
[fuatsezer@localhost kafka]$ bin/zookeeper-server-start.sh  -daemon config/zookeeper.properties
[fuatsezer@localhost kafka]$ sudo chmod 755 bin
[fuatsezer@localhost kafka]$ cd bin/
[fuatsezer@localhost bin]$ sudo chmod 755 *.sh
[fuatsezer@localhost bin]$ ls -l
[fuatsezer@localhost bin]$ cd ..
[fuatsezer@localhost bin]$ sudo chown -R fuatsezer .
[fuatsezer@localhost kafka]$ bin/zookeeper-server-start.sh  -daemon config/zookeeper.properties
[fuatsezer@localhost kafka]$ bin/kafka-server-start.sh -daemon config/server.properties
```
Aşağıdaki komut ile bellek boyutunu ayarlayabilirsiniz
```console
[fuatsezer@localhost kafka]$ export KAFKA_HEAP_OPTS="-Xmx1G -Xms1G"
```
## Zookeper ve Kafka servislerini Durdurma
```console
[fuatsezer@localhost kafka]$ bin/kafka-server-stop.sh
[fuatsezer@localhost kafka]$ bin/zookeeper-server-stop.sh
```



