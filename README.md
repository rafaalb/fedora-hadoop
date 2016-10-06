
Installation instructions (Fedora Commons 3.6.2, Hadoop Cloudera 5):
---------------------------------------------------------------
Configuramos el archivo fedora.fcfg para utilizar el almacenamieto por defecto akubra-hdfs.

Se encuentra en el folder $FEDORA_HOME/server/config/fedora.fcfg

Al clonar el proyecto debemos instalarlo con maven con el siguiente comando:

mvn install

#Nos genera un .jar llamado akubra-hdfs-0.0.1-SNAPSHOT.jar en el folder target

### Dependencies
Copiar las dependencias de Hadoop al siguiente directorio de Fedora:
$FEDORA_HOME/tomcat/webapps/fedora/WEB-INF/lib

* akubra-hdfs-0.0.1-SNAPSHOT.jar
* hadoop-core-1.0.3.jar from $HADOOP_HOME/
* hadoop-client-1.0.3.jar from $HADOOP_HOME/
* commons-configuration-1.6.jar from $HADOOP_HOME/lib/
* commons-lang-2.4.jar from $HADOOP_HOME/lib/ 
* htrace-core4-4.0.1-incubating.jar 
* hadoop-hdfs-2.6.0-cdh5.8.0.jar 
* hadoop-auth-2.6.0-cdh5.8.0.jar
* akubra-hdfs-0.0.1-SNAPSHOT.jar


### Configuracion

En el archivo:  ```$FEDORA_HOME/server/config/spring/akubra-llstore.xml``` 
Editamos los beans: ```fsObjectStore``` and ```fsDataStreamStore```



	<bean name="fsObjectStore" class="de.fiz.akubra.hdfs.HDFSBlobStore" singleton="true">
		<constructor-arg value="hdfs://<ruta>:8020/fedora/objects"/>
	</bean>
	
	<bean name="fsObjectStoreMapper" class="de.fiz.akubra.hdfs.HDFSIdMapper" singleton="true">
		<constructor-arg ref="fsObjectStore"/>
	</bean>


	<bean name="fsDatastreamStore" class="de.fiz.akubra.hdfs.HDFSBlobStore" singleton="true">
		<constructor-arg value="hdfs://<ruta>:8020/fedora/datastreams"/>
	</bean>

	<bean name="fsDatastreamStoreMapper" class="de.fiz.akubra.hdfs.HDFSIdMapper" singleton="true">
		<constructor-arg ref="fsDatastreamStore"/>
	  </bean>


### License

akubra-hdfs is licensed under the [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0)
