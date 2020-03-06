---
title: Configurar a segurança do Hadoop do polybase
description: Explica como configurar o polybase em paralelo data warehouse para se conectar ao Hadoop externo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/26/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f275c77556e8abe8932e241075b9e24e2ae5db77
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78340458"
---
# <a name="polybase-configuration-and-security-for-hadoop"></a>Configuração e segurança do PolyBase para Hadoop

Este artigo fornece uma referência para várias definições de configuração que afetam a conectividade do polybase do APS com o Hadoop. Para obter instruções sobre o que é o polybase, consulte [o que é o polybase](configure-polybase-connectivity-to-external-data.md).

> [!NOTE]
> No APS, as alterações em arquivos XML são necessárias em todos os nós de computação e no nó de controle.
> 
> Tome cuidado especial ao modificar arquivos XML no APS. Quaisquer marcas ausentes ou caracteres indesejados podem invalidar o arquivo XML, impedindo o usablilty do recurso.
> Os arquivos de configuração do Hadoop estão localizados no seguinte caminho:  
> ```  
> C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf 
> ``` 
> As alterações nos arquivos XML exigem a reinicialização do serviço para entrar em vigor.

## <a id="rpcprotection"></a>Configuração do Hadoop. RPC. Protection

Uma maneira comum de proteger a comunicação em um cluster Hadoop é alterando a configuração de hadoop.rpc.protection para “Privacidade” ou “Integridade”. Por padrão, o PolyBase assume que a configuração está definida como 'Autenticar'. Para substituir esse padrão, adicione a propriedade a seguir ao arquivo core-site.xml. A alteração dessa configuração permitirá a transferência de dados segura entre os nós do Hadoop e a conexão SSL com o SQL Server.

```xml
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
   <property>
     <name>hadoop.rpc.protection</name>
     <value></value>
   </property> 
```

## <a id="kerberossettings"></a>Configuração do Kerberos  

Observe que, quando o PolyBase é autenticado em um cluster protegido pelo Kerberos, ele espera que a configuração de hadoop.rpc.protection seja 'Autenticar' por padrão. Isso faz com que a comunicação de dados entre os nós do Hadoop não seja criptografada. Para usar as configurações de 'Privacidade' ou 'Integridade' para o hadoop.rpc.protection, atualize o arquivo core-site.xml no servidor do PolyBase. Para obter mais informações, confira a seção anterior [Conectando-se ao cluster Hadoop com a configuração Hadoop.rpc.protection](#rpcprotection).

Para se conectar a um cluster Hadoop protegido por Kerberos usando MIT KDC, as seguintes alterações são necessárias em todos os nós de computação APS e no nó de controle:

1. Localize os diretórios de configuração do Hadoop no caminho de instalação do APS. Normalmente, o caminho é:  

   ```  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf  
   ```  

2. Localize o valor de configuração do lado do Hadoop nas chaves de configuração listadas na tabela. (No computador do Hadoop, localize os arquivos no diretório da configuração do Hadoop.)  
   
3. Copie os valores de configuração na propriedade de valor nos arquivos correspondentes no computador do SQL Server.  
   
   |**#**|**Arquivo de configuração**|**Chave de configuração**|**Ação**|  
   |------------|----------------|---------------------|----------|   
   |1|core-site.xml|polybase.kerberos.kdchost|Especifique o nome de host do KDC. Por exemplo: kerberos.your-realm.com.|  
   |2|core-site.xml|polybase.kerberos.realm|Especifique o realm do Kerberos. Por exemplo: YOUR-REALM.COM|  
   |3|core-site.xml|hadoop.security.authentication|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: KERBEROS<br></br>**Observação de segurança:** O KERBEROS deve ser escrito em letras maiúsculas. Se for escrito em letras minúsculas, talvez ele não seja ativado.|   
   |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: hdfs/_HOST@YOUR-REALM.COM|  
   |5|mapred-site.xml|mapreduce.jobhistory.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: mapred/_HOST@YOUR-REALM.COM|  
   |6|mapred-site.xml|mapreduce.jobhistory.address|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: 10.193.26.174:10020|  
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

## <a id="encryptionzone"></a>Configuração da zona de criptografia do Hadoop
Se você estiver usando a zona de criptografia do Hadoop, modifique Core-site. xml e HDFS-site. XML da seguinte maneira. Forneça o endereço IP em que o serviço KMS está sendo executado com o número da porta correspondente. A porta padrão para o KMS no CDH é 16000.

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