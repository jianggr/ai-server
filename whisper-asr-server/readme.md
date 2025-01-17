## whipser-asr-server
### 在线文档
https://apifox.com/apidoc/shared-98cc5675-f1a3-4250-a940-cfe060854ef4/api-121475073

### 接口
#### 测试接口
访问地址:http://localhost/whispser/asr/rec  
返回数据
```
{
    "data": [
        {
            "end": 1088,
            "sentence": " And so, my fellow Americans, ask not what your country can do for you, ask what you can do for your country.",
            "start": 0
        }
    ],
    "ok": true
}
```

### build
```
# Set java version
export JAVA_HOME=/usr/java/jdk-11.0.8
export PATH=$JAVA_HOME/bin:$PATH

#build jar
mvn clean install -DskipTests -Pdevelopment
mvn clean package -DskipTests -Pproduction -pl ai-server-tio-boot
```
### run
```
java -jar ai-server-tio-boot/target/ai-server-tio-boot-1.0.jar --mode=pord
```
The default loaded model is `/root/.cache/whisper/ggml-base.en.bin`


specify the model name
```
java -jar ai-server-tio-boot/target/ai-server-tio-boot-1.0.jar --mode=pord --model.name=ggml-large.bin
```

### test
```
curl http://localhost:10046/asr/test
```

### 构建Docker镜像
### 封装镜像

build

```
docker build -f docker/1.0.0-base.en -t litongjava/ai-server:1.0.1-base.en .
```

run

```
docker run -dit -p 10046:10046 litongjava/ai-server:1.0.1-base.en
```

test

```
curl -v http://localhost:10046/asr/test
```
build large
```
docker build -f docker/1.0.0-large -t litongjava/ai-server:1.0.1-large .
```

```
docker run -dit -p 10046:10046 litongjava/ai-server:1.0.1-large
```
