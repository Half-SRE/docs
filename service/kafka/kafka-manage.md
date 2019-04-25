kafka管理工具: [yahoo kafka-manage](https://github.com/yahoo/kafka-manager)

主要步骤：
- 安装
- 管理

**1.安装依赖工具sbt**
```
curl -o /etc/yum.repo.d/bintray-sbt-rpm.repo https://bintray.com/sbt/rpm/rpm
yum -y install sbt
```  

安装失败，官网源302错误，更换阿里源  
```
mkdir ~/.sbt

vim ~/.sbt/repositories
[repositories]
local
aliyun: http://maven.aliyun.com/nexus/content/groups/public/
typesafe: http://repo.typesafe.com/typesafe/ivy-releases/, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext], bootOnly
sonatype-oss-releases
maven-central
sonatype-oss-snapshots
```  

再次安装sbt即可。  

**2.编译kafka-manage源码包**  

下载源码包
```
git clone https://github.com/yahoo/kafka-manager.git
```  

编译
```
kafka-manager-2.0.0.2/sbt clean dist
```  

编译完成后在`target/universal/kafka-manager-2.0.0.2.zip`生成zip包，解压后mv至`/data/app/`  

**3.启动kafka-manage**  
```
bin/kafka-manager -Dpidfile.path=/data/pid/kafka-manage.pid -Dhttp.port=9000 -Dhttp.address=0.0.0.0
服务在终端前台运行
```  
> 注意修改log级别，默认info  

结尾，前端使用nginx代理验证，kafka-manage支持openldap。
