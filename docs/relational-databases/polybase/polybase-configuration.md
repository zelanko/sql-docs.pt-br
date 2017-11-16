---
title: "Configuração do PolyBase | Microsoft Docs"
ms.custom: 
ms.date: 09/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80ff73c1-2861-438b-a13f-309155f3d6e1
caps.latest.revision: "17"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a750d1dbc4adb1dbd09fb718dd05a81661381a8c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="polybase-configuration"></a>Configuração do PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Use os procedimentos a seguir para configurar o PolyBase.  
  
## <a name="external-data-source-configuration"></a>Configuração da fonte de dados externa  
 Garanta conectividade com a fonte de dados externa no SQL Server. O tipo de conectividade influencia consideravelmente o desempenho da consulta. Por exemplo, um link Ethernet de 10 Gbit resultará em um menor tempo de resposta para consultas do PolyBase do que um link Ethernet de 1 Gbit.  
  
 É necessário configurar o SQL Server para se conectar com a versão do Hadoop ou do armazenamento de Blobs do Azure usando **sp_configure**. O PolyBase oferece suporte a duas distribuições do Hadoop: HDP (Hortonworks Data Platform) e CDH (Cloudera Distributed Hadoop).  Para obter uma lista completa de fontes de dados externas com suporte, veja [Configuração de conectividade do PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
1 Observação: o PolyBase não dá suporte a Zonas Criptografadas do Cloudera. 
  
### <a name="run-spconfigure"></a>Executar sp_configure  
  
1.  Execute sp_configure “conectividade hadoop” e defina um valor apropriado.  Para encontrar o valor, veja [Configuração do PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
    ```tsql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  É necessário reiniciar o SQL Server usando **services.msc**. A reinicialização do o SQL Server reiniciará estes serviços:  
  
    -   Serviço de movimentação de dados de PolyBase do SQL Server  
  
    -   Mecanismo PolyBase do SQL Server  
  
## <a name="pushdown-configuration"></a>Configuração de empilhamento  
 Para melhorar o desempenho da consulta, habilite a computação de aplicação para um cluster de Hadoop. Será necessário fornecer ao SQL Server alguns parâmetros de configuração específicos para seu ambiente de Hadoop:  
  
1.  Localize o arquivo **yarn-site.xml** no caminho de instalação do SQL Server. Normalmente, o caminho é:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  No computador do Hadoop, localize o arquivo análogo no diretório da configuração do Hadoop. No arquivo, localize e copie o valor da chave de configuração yarn.application.classpath.  
  
3.  No computador do SQL Server, no **yarn.site.xml file,** localize a propriedade **yarn.application.classpath** . Cole o valor do computador do Hadoop no elemento de valor.  

4. Para todas as versões do CDH 5.X, você precisará adicionar os parâmetros de configuração **mapreduce.application.classpath** ao final do **arquivo yarn.site.xml** ou ao **arquivo mapred-site.xml**. O HortonWorks inclui essas configurações nas configurações **yarn.application.classpath**.

## <a name="connecting-to-hadoop-cluster-with-hadooprpcprotection-setting"></a>Conectando-se ao cluster Hadoop com a configuração Hadoop.RPC.Protection
Uma maneira comum de proteger a comunicação em um cluster Hadoop é alterando a configuração de hadoop.rpc.protection para “Privacidade” ou “Integridade”. Por padrão, o PolyBase pressupõe que a configuração está definida como “Autenticar”. Para substituir esse padrão, você precisa adicionar a propriedade a seguir ao arquivo core-site.xml. A alteração dessa configuração permitirá a transferência de dados segura entre os nós do Hadoop, bem como a conexão SSL com o SQL Server.

```
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
  <property>
    <name>hadoop.rpc.protection</name>
    <value></value>
  </property> 
```




## <a name="example-yarn-sitexml-and-mapred-sitexml-files-for-cdh-5x-cluster"></a>Arquivos yarn-site.xml e mapred-site.xml de exemplo para cluster CDH 5.X.



Configuração de yarn-site.xml com yarn.application.classpath e mapreduce.application.classpath.
```
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
Se você optar por dividir as duas definições de configuração no mapred-site.xml e no yarn-site.xml, os arquivos seriam os seguintes:

**yarn-site.xml**
```
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

```
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
Observe que quando PolyBase se autentica em um cluster protegido por Kerberos, precisamos que a configuração hadoop.rpc.protection seja definida para autenticação. Isso manterá a comunicação de dados entre os nós do Hadoop não criptografados. 

 Para se conectar a um cluster Hadoop protegido por Kerberos [usando MIT KDC]:
   
  
1.  Localize o diretório de configuração do Hadoop no caminho de instalação do SQL Server. Normalmente, o caminho é:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  Localize o valor de configuração do lado do Hadoop nas chaves de configuração listadas na tabela. (No computador do Hadoop, localize os arquivos no diretório da configuração do Hadoop.)  
  
3.  Copie os valores de configuração na propriedade de valor nos arquivos correspondentes no computador do SQL Server.  
  
    |**#**|**Arquivo de configuração**|**Chave de configuração**|**Ação**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|Especifique o nome de host do KDC. Por exemplo: kerberos.your-realm.com.|  
    |2|core-site.xml|polybase.kerberos.realm|Especifique o realm do Kerberos. Por exemplo: YOUR-REALM.COM|  
    |3|core-site.xml|hadoop.security.authentication|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: KERBEROS<br></br>**Observação de segurança:** KERBEROS deve ser escrito em letras maiúsculas. Se for escrito em letras minúsculas, talvez ele não seja ativado.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: 10.193.26.174:10020|  
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: yarn/_HOST@YOUR-REALM.COM|  
  
4.  Crie um objeto de credencial com escopo de banco de dados para especificar as informações de autenticação de cada usuário do Hadoop. Veja [Objetos T-SQL do PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md).  
  
## <a name="next-steps"></a>Próximas etapas  
 [Objetos T-SQL do PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md)  
  
 [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)  
  
## <a name="see-also"></a>Consulte também  
 [Configuração de conectividade do PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)   
 [Guia do PolyBase](../../relational-databases/polybase/polybase-guide.md)  
  
  
