# Test-DevoOps-Microservices-Billing

## Azure DevOps

### Integrar Azure DevOps Artifacs

1.- Agregar la dependencia del artefacto que desarrollamos en el proyecto "common" en el archivo pom.xml como se muestra a continuacion.-

```xml
<dependency>
  <groupId>com.digitalthinking</groupId>
  <artifactId>common-library</artifactId>
  <version>0.0.2-SNAPSHOT</version>
</dependency>
```

2.- Configuramos el servidor de artefactos en el archivo pom.xml.-

```xml
<repository>
  <id>Common_Artifac</id>
  <url>https://pkgs.dev.azure.com/paulo866/56086bd2-562a-4422-a346-2e7d375f05af/_packaging/Common_Artifac/maven/v1</url>
  <releases>
    <enabled>true</enabled>
  </releases>
  <snapshots>
    <enabled>true</enabled>
  </snapshots>
</repository>
```

3.- Configuramos el servidor de artefactos en el settings.xml, este archivo se encuentra en archivo ~/.m2.-

```xml
<server>
    <id>Common_Artifac</id>
    <username>paulo866</username>
    <password>[PERSONAL_ACCESS_TOKEN]</password>
</server>
```

3.1.- Configuracion en codespaces (github) para configurar el archivo settings.xml y ~/.m2.-

Para ver el path de instalacion de maven corremos el siguiente comando.-

```
echo $MAVEN_HOME
```

Para poder trabajar con el archivo settingd.xml, lo copiamos utilizando el siguiente comando.-

```
cp $MAVEN_HOME/conf/settings.xml ~/.m2
```

Listo ya podemos empezar a configurar el archivo para lograr la conexion.

4.- Reconfiguramos el proyecto para agregar el artefacto.-

```
mvn -X -P azure_artifacts package
```

### Error al correr el comando "mvn -X -P azure_artifacts package" en MAC.-

En Maven carga su propio JAVA_HOME desde la ruta especificada en: ~/.mavenrc

Cambié el contenido del archivo para que sea parecido al siguiente.-

```
JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_45.jdk/Contents/Home
```