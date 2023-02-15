## 依赖引用
这是一个common utility的包,其他项目会依赖于这个包,所以在更改后,需要把snapshot的库更新以下,以便其他项目可以依赖到最新的包.

```
mvn deploy:deploy-file -DgroupId=com.mbp.eng -DartifactId=common.util -Dversion=1.0.0-SNAPSHOT -Dpackaging=jar -Dfile=./target/common.util-1.0.0-SNAPSHOT.jar -Durl=http://xxx.xxx.com/snapshots/ -DrepositoryId=snapshots
```

release:
```bash
mvn deploy:deploy-file -DgroupId=com.mbp.eng -DartifactId=common.util -Dversion=1.0.0-SNAPSHOT -Dpackaging=jar -Dfile=./target/common.util-1.0.0-SNAPSHOT.jar -Durl=http://xxx.xxx.com/releases/ -DrepositoryId=releases
```