---
title: "Configura&#231;&#227;o do PolyBase | Microsoft Docs"
ms.custom: ""
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 80ff73c1-2861-438b-a13f-309155f3d6e1
caps.latest.revision: 17
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 12
---
# Configura&#231;&#227;o do PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Use os procedimentos a seguir para configurar o PolyBase.  
  
## <a name="external-data-source-configuration"></a>Configuração da fonte de dados externa  
 Garanta conectividade com a fonte de dados externa no SQL Server. O tipo de conectividade influencia consideravelmente o desempenho esperado da consulta. Por exemplo, um link Ethernet de 10 Gbit resultará em um menor tempo de resposta para consultas do PolyBase do que um link Ethernet de 1 Gbit.  
  
 É necessário configurar o SQL Server para se conectar com a versão do Hadoop ou do armazenamento de Blobs do Azure usando **sp_configure**. O PolyBase oferece suporte a duas distribuições do Hadoop: HDP (Hortonworks Data Platform) e CDH (Cloudera Distributed Hadoop).  Para obter uma lista completa de fontes de dados externas com suporte, veja [Configuração de conectividade do PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
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
 Para melhorar o desempenho da consulta, habilite a computação de aplicação para um cluster Hadoop:  
  
1.  Localize o arquivo **yarn-site.xml** no caminho de instalação do SQL Server. Normalmente, o caminho é:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  No computador do Hadoop, localize o arquivo análogo no diretório da configuração do Hadoop. No arquivo, localize e copie o valor da chave de configuração yarn.application.classpath.  
  
3.  No computador do SQL Server, no **yarn.site.xml file,** localize a propriedade **yarn.application.classpath**. Cole o valor do computador do Hadoop no elemento de valor.  
  
## <a name="kerberos-configuration"></a>Configuração do Kerberos  
 Para se conectar a um cluster Hadoop protegido por Kerberos [usando MIT KDC]:  
  
1.  Localize o diretório de configuração do Hadoop no caminho de instalação do SQL Server. Normalmente, o caminho é:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  Localize o valor de configuração do lado do Hadoop nas chaves de configuração listadas na tabela. (No computador do Hadoop, localize os arquivos no diretório da configuração do Hadoop.)  
  
3.  Copie os valores de configuração na propriedade de valor nos arquivos correspondentes no computador do SQL Server.  
  
    |**#**|**Arquivo de configuração**|**Chave de configuração**|**Ação**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|Especifique o realm do Kerberos. Por exemplo: YOUR-REALM.COM|  
    |2|core-site.xml|polybase.kerberos.realm|Especifique o nome de host do KDC. Por exemplo: kerberos.your-realm.com.|  
    |3|core-site.xml|hadoop.security.authentication|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: KERBEROS<br></br>**Observação de segurança:** KERBEROS deve ser escrito em letras maiúsculas. Se for escrito em letras minúsculas, talvez ele não seja ativado.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.address|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: 10.193.26.174:10020|  
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: yarn/_HOST@YOUR-REALM.COM|  
  
4.  Crie um objeto de credencial com escopo de banco de dados para especificar as informações de autenticação de cada usuário do Hadoop. Veja [Objetos T-SQL do PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md).  
  
## <a name="next-steps"></a>Próximas etapas  
 [Objetos T-SQL do PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md)  
  
 [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)  
  
## <a name="see-also"></a>Consulte também  
 [Configuração de conectividade do PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)   
 [Guia do PolyBase](../../relational-databases/polybase/polybase-guide.md)  
  
  