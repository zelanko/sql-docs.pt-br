---
title: Configurar a segurança de PolyBase Hadoop no Analytics Platform System | Microsoft Docs
description: Explica como configurar o PolyBase no Parallel Data Warehouse para se conectar ao Hadoop externo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/26/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c916fef2b70333c2d5bc89fec5c86d61482cdba7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678604"
---
# <a name="polybase-configuration-and-security-for-hadoop"></a>Configuração e segurança do PolyBase para Hadoop

Este artigo fornece uma referência para várias configurações que afetam a conectividade do PolyBase de APS para Hadoop. Para obter uma explicação sobre o que é PolyBase, consulte [o que é PolyBase](configure-polybase-connectivity-to-external-data.md).

> [!NOTE]
> No APS, alterações em arquivos XML são necessários em todos os nós de computação e o nó de controle.
> 
> Tome um cuidado especial ao modificar arquivos XML no APS. Quaisquer marcas ausentes ou caracteres indesejados podem invalidar o arquivo xml obstruindo o usablilty do recurso.
> Arquivos de configuração do Hadoop estão localizados no seguinte caminho:  
> ```  
> C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf 
> ``` 
> Todas as alterações nos arquivos xml exigem uma reinicialização do serviço para ser eficaz.

## <a id="rpcprotection"></a> Configuração Hadoop.RPC.Protection

Uma maneira comum de proteger a comunicação em um cluster Hadoop é alterando a configuração de hadoop.rpc.protection para “Privacidade” ou “Integridade”. Por padrão, o PolyBase assume que a configuração está definida como 'Autenticar'. Para substituir esse padrão, adicione a propriedade a seguir ao arquivo core-site.xml. A alteração dessa configuração permitirá a transferência de dados segura entre os nós do Hadoop e a conexão SSL com o SQL Server.

```xml
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
   <property>
     <name>hadoop.rpc.protection</name>
     <value></value>
   </property> 
```

## <a name="example-xml-files-for-cdh-5x-cluster"></a>Arquivos XML de exemplo para cluster do CDH 5.X

Configuração de yarn-site.xml com yarn.application.classpath e mapreduce.application.classpath.

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
   <property>
      <name>yarn.resourcemanager.connect.max-wait.ms</name>
      <value>40000</value>
   </property>
   <property>
      <name>yarn.resourcemanager.connect.retry-interval.ms</name>
      <value>30000</value>
   </property>
<!-- Applications' Configuration-->
   <property>
     <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
      <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
      <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
      <name>yarn.application.classpath</name>
      <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/,$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH*</value>
   </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
      <name>yarn.resourcemanager.principal</name>
      <value></value>
   </property>
-->
</configuration>
```

Se você optar por dividir as duas configurações em mapred-site. XML e o yarn-site. XML, os arquivos seria o seguinte:

**yarn-site.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
   <property>
      <name>yarn.resourcemanager.connect.max-wait.ms</name>
      <value>40000</value>
   </property>
   <property>
      <name>yarn.resourcemanager.connect.retry-interval.ms</name>
      <value>30000</value>
   </property>
<!-- Applications' Configuration-->
   <property>
     <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
      <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
      <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
      <name>yarn.application.classpath</name>
      <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/*</value>
   </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
      <name>yarn.resourcemanager.principal</name>
      <value></value>
   </property>
-->
</configuration>
```

**mapred-site.xml**

Observe que adicionamos a propriedade mapreduce.application.classpath. No CDH 5.x, você encontrará os valores de configuração com a mesma convenção de nomenclatura no Ambari.

```xml
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration xmlns:xi="http://www.w3.org/2001/XInclude">
   <property>
     <name>mapred.min.split.size</name>
       <value>1073741824</value>
   </property>
   <property>
     <name>mapreduce.app-submission.cross-platform</name>
     <value>true</value>
   </property>
<property>
     <name>mapreduce.application.classpath</name>
     <value>$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH</value>
   </property>


<!--kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
     <name>mapreduce.jobhistory.principal</name>
     <value></value>
   </property>
   <property>
     <name>mapreduce.jobhistory.address</name>
     <value></value>
   </property>
-->
</configuration>
```

## <a name="kerberos-configuration"></a>Configuração do Kerberos  

Observe que, quando o PolyBase é autenticado em um cluster protegido pelo Kerberos, ele espera que a configuração de hadoop.rpc.protection seja 'Autenticar' por padrão. Isso faz com que a comunicação de dados entre os nós do Hadoop não seja criptografada. Para usar as configurações de 'Privacidade' ou 'Integridade' para o hadoop.rpc.protection, atualize o arquivo core-site.xml no servidor do PolyBase. Para obter mais informações, confira a seção anterior [Conectando-se ao cluster Hadoop com a configuração Hadoop.rpc.protection](#rpcprotection).

Para se conectar a um Hadoop protegido por Kerberos cluster usando MIT KDC as seguintes alterações são necessárias no APS todos os nós de computação e nó de controle:

1. Localize os diretórios de configuração do Hadoop no caminho de instalação do APS. Normalmente, o caminho é:  

   ```  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf  
   ```  

2. Localize o valor de configuração do lado do Hadoop nas chaves de configuração listadas na tabela. (No computador do Hadoop, localize os arquivos no diretório da configuração do Hadoop.)  
   
3. Copie os valores de configuração na propriedade de valor nos arquivos correspondentes no computador do SQL Server.  
   
   |**#**|**Arquivo de configuração**|**Chave de configuração**|**Ação**|  
   |------------|----------------|---------------------|----------|   
   |1|core-site.xml|polybase.kerberos.kdchost|Especifique o nome de host do KDC. Por exemplo: kerberos.your-realm.com.|  
   |2|core-site.xml|polybase.kerberos.realm|Especifique o realm do Kerberos. Por exemplo:  YOUR-REALM.COM|  
   |3|core-site.xml|hadoop.security.authentication|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: KERBEROS<br></br>**Observação de segurança:** KERBEROS deve ser escrito em letras maiúsculas. Se for escrito em letras minúsculas, talvez ele não seja ativado.|   
   |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: hdfs/_HOST@YOUR-REALM.COM|  
   |5|mapred-site.xml|mapreduce.jobhistory.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: mapred/_HOST@YOUR-REALM.COM|  
   |6|mapred-site.xml|mapreduce.jobhistory.address|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo:  10.193.26.174:10020|  
   |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: yarn/_HOST@YOUR-REALM.COM|  

**core-site.xml**
```xml
<property>
  <name>polybase.kerberos.realm</name>
  <value></value>
</property>
<property>
  <name>polybase.kerberos.kdchost</name>
  <value></value>
</property>
<property>
    <name>hadoop.security.authentication</name>
    <value>KERBEROS</value>
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.namenode.kerberos.principal</name>
  <value></value> 
</property>
```

**mapred-site.xml**
```xml
<property>
  <name>mapreduce.jobhistory.principal</name>
  <value></value>
</property>
<property>
  <name>mapreduce.jobhistory.address</name>
  <value></value>
</property>
```

**yarn-site.xml**
```xml
<property>
  <name>yarn.resourcemanager.principal</name>
  <value></value>
</property>
```

4. Crie um objeto de credencial com escopo de banco de dados para especificar as informações de autenticação de cada usuário do Hadoop. Veja [Objetos T-SQL do PolyBase](../relational-databases/polybase/polybase-t-sql-objects.md).

## <a id="encryptionzone"></a> Configuração da zona de criptografia do Hadoop
Se você estiver usando o Hadoop zona de criptografia modificar core-site. XML e hdfs-site. XML da seguinte maneira. Forneça o endereço ip em que o serviço KMS está em execução com o número da porta correspondente. A porta padrão do KMS no CDH é 16000.

**core-site.xml**
```xml
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value> 
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.encryption.key.provider.uri</name>
  <value>kms://http@<ip address>:16000/kms</value>
</property>
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value>
  </property>
```