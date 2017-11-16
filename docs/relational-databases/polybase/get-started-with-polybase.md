---
title: "Introdução ao PolyBase | Microsoft Docs"
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- PolyBase
- PolyBase, getting started
- Hadoop import
- Hadoop export
- Azure blob storage import
- Azure blob storage export
- Hadoop import, PolyBase getting started
- Hadoop export, Polybase getting started
caps.latest.revision: 78
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 74f73ab33a010583b4747fcc2d9b35d6cdea14a2
ms.openlocfilehash: b107ea3ebabbf959ee12b900885612df364dfc12
ms.contentlocale: pt-br
ms.lasthandoff: 08/04/2017

---
# <a name="get-started-with-polybase"></a>Introdução ao PolyBase
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico contém as noções básicas sobre a execução do PolyBase em uma instância do SQL Server.
  
 Depois de executar as etapas a seguir, você terá:  
  
-   O PolyBase instalado e executável no servidor  
  
-   Exemplos de instruções que criam objetos PolyBase  
  
-   Um entendimento de como gerenciar objetos PolyBase no SSMS (SQL Server Management Studio)  
  
-   Exemplos de consultas que usam objetos PolyBase  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Uma instância do [SQL Server (64 bits)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) com o seguinte:  
  
-   Microsoft .NET Framework 4.5.  
  
-   Oracle JRE (Java SE RunTime Environment) versão 7.51 ou superior (64 bits). (Qualquer [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) ou [servidor JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) funcionará). Vá para [Downloads de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/index.html). O instalador falhará se o JRE não estiver presente.   
  
-   Memória mínima: 4 GB  
  
-   Espaço mínimo no disco rígido: 2 GB    

-   A conectividade TCP/IP deve estar habilitada. (Veja [Habilitar ou desabilitar um protocolo de rede de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).) As edições do SQL Server Developer e Express têm o TCP/IP desabilitado por padrão. O PolyBase pode ser instalado, mas não será totalmente iniciado até que o TCP/IP esteja habilitado. Você deve habilitar manualmente o TCP/IP para ter a funcionalidade PolyBase. 
  
 
 Uma fonte de dados externa, uma das seguintes:  
  
-   Cluster do Hadoop. Para obter as versões com suporte, veja [Configurar o PolyBase](#supported).  

-   Armazenamento de blobs do Azure

> [!NOTE]
>   Se pretender usar a funcionalidade de pushdown de computação contra Hadoop, você precisará garantir que o cluster do Hadoop de destino tenha componentes principais do HDFS, Yarn/MapReduce com o servidor Jobhistory habilitado. O PolyBase envia a consulta de aplicação via MapReduce e recebe o status do servidor JobHistory. A consulta falhará se não tiver um desses componentes. 

## <a name="install-polybase"></a>Instalar o PolyBase  
 Se você ainda não instalou o PolyBase, consulte [Instalação do PolyBase](../../relational-databases/polybase/polybase-installation.md).  
  
### <a name="how-to-confirm-installation"></a>Como confirmar a instalação  
 Após a instalação, execute o comando a seguir para confirmar que o PolyBase foi instalado com êxito. Se o PolyBase estiver instalado, retornará 1; caso contrário, 0.  
  
```tsql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
##  <a name="supported"></a> Configurar o PolyBase  
 Após a instalação, você deve configurar o SQL Server para usar a versão do Hadoop ou Armazenamento de Blobs do Azure. O PolyBase é compatível com dois provedores de Hadoop, HDP (Hortonworks Data Platform) e CDH (Cloudera Distributed Hadoop).  As fontes de dados externas compatíveis incluem:  
  
-   Hortonworks HDP 1.3 em Linux/Windows Server  
  
-   Hortonworks HDP 2.1 – 2.6 no Linux

-   Hortonworks HDP 2.1 a 2.3 no Windows Server  
  
-   Cloudera CDH 4.3 em Linux  
  
-   Cloudera CDH 5.1 – 5.5, 5.9 – 5.12 em Linux  
  
-   Armazenamento de blobs do Azure  
 
O Hadoop segue o padrão de "Major.Minor.Version" para suas novas versões. Há suporte para todas as versões em uma versão Major e Minor com suporte.
 

>  [!NOTE]
> Somente há suporte para conectividade do Azure Data Lake Store no SQL Data Warehouse do Azure.
  
### <a name="external-data-source-configuration"></a>Configuração da fonte de dados externa  
  
1.  Execute [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) “conectividade hadoop” e defina um valor apropriado. Por padrão, a conectividade de hadoop é definida como 7. Para encontrar o valor, veja [Configuração do PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
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
  
 ![Parar e iniciar serviços de PolyBase em services.msc](../../relational-databases/polybase/media/polybase-stop-start.png "Parar e iniciar serviços de PolyBase em services.msc")  
  
### <a name="pushdown-configuration"></a>Configuração de empilhamento  
 Para melhorar o desempenho da consulta, habilite a computação de aplicação para um cluster Hadoop:  
  
1.  Localize o arquivo **yarn-site.xml** no caminho de instalação do SQL Server. Normalmente, o caminho é:  
  
    ```  
  
    C:Program FilesMicrosoft SQL ServerMSSQL13.MSSQLSERVERMSSQLBinnPolybaseHadoopconf  
  
    ```  
  
2.  No computador do Hadoop, localize o arquivo análogo no diretório da configuração do Hadoop. No arquivo, localize e copie o valor da chave de configuração yarn.application.classpath.  
  
3.  No computador do SQL Server, no **yarn.site.xml file,** localize a propriedade **yarn.application.classpath** . Cole o valor do computador do Hadoop no elemento de valor.  
  
4. Para todas as versões do CDH 5.X, você precisará adicionar os parâmetros de configuração mapreduce.application.classpath ao final do arquivo yarn.site.xml ou ao arquivo mapred-site.xml. O HortonWorks inclui essas configurações nas configurações yarn.application.classpath. Veja [Configuração do PolyBase](../../relational-databases/polybase/polybase-configuration.md) para obter exemplos.

 
## <a name="scale-out-polybase"></a>Escalar o PolyBase horizontalmente  
 O recurso de grupo do PolyBase permite criar um cluster de instâncias do SQL Server para processar grandes conjuntos de dados de fontes de dados externas de maneira escalar horizontal para melhor desempenho de consulta.  
  
1.  Instale o SQL Server com o PolyBase em vários computadores.  
  
2.  Selecione um SQL Server como nó de cabeçalho.  
  
3.  Adicione outras instâncias como nós de computação executando [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
4.  Reinicie o Serviço de Movimentação de Dados do PolyBase nos nós de computação.  
  
 Para obter detalhes, veja [Grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).  
  
## <a name="create-t-sql-objects"></a>Criar objetos T-SQL  
 Crie objetos dependendo da fonte de dados externa, armazenamento do Azure ou Hadoop.  
  
### <a name="hadoop"></a>Hadoop  
  
```sql  
-- 1: Create a database scoped credential.  
-- Create a master key on the database. This is required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- 2: Create a database scoped credential  for Kerberos-secured Hadoop clusters.  
-- IDENTITY: the Kerberos user name.  
-- SECRET: the Kerberos password  
  
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1   
WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
  
-- 3:  Create an external data source.  
-- LOCATION (Required) : Hadoop Name Node IP address and port.  
-- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
-- CREDENTIAL (Optional):  the database scoped credential, created above.  
  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
        TYPE = HADOOP,   
        LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',   
        RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',   
        CREDENTIAL = HadoopUser1        
);  
  
-- 4: Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).    
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
-- 5:  Create an external table pointing to data stored in Hadoop.  
-- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
  
CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
        [SensorKey] int NOT NULL,   
        [CustomerKey] int NOT NULL,   
        [GeographyKey] int NULL,   
        [Speed] float NOT NULL,   
        [YearMeasured] int NOT NULL  
)  
WITH (LOCATION='/Demo/',   
        DATA_SOURCE = MyHadoopCluster,  
        FILE_FORMAT = TextFileFormat  
);  
  
-- 6:  Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
### <a name="azure-blob-storage"></a>Armazenamento de blobs do Azure  
  
```sql  
--1: Create a master key on the database.  
-- Required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- Create a database scoped credential  for Azure blob storage.  
-- IDENTITY: any string (this is not used for authentication to Azure storage).  
-- SECRET: your Azure storage account key.  
  
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential   
WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';  
  
--2:  Create an external data source.  
-- LOCATION:  Azure account storage account name and blob container name.  
-- CREDENTIAL: The database scoped credential created above.  
  
CREATE EXTERNAL DATA SOURCE AzureStorage with (  
        TYPE = HADOOP,   
        LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
        CREDENTIAL = AzureStorageCredential  
);  
  
--3:  Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH (  
       FORMAT_TYPE = DELIMITEDTEXT,   
       FORMAT_OPTIONS (
         FIELD_TERMINATOR ='|',   
         USE_TYPE_DEFAULT = TRUE
       )
);
         
  
--4: Create an external table.  
-- The external table points to data stored in Azure storage.  
-- LOCATION: path to a file or directory that contains the data (relative to the blob container).  
-- To point to all files under the blob container, use LOCATION='/'   
  
CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
        [SensorKey] int NOT NULL,   
        [CustomerKey] int NOT NULL,   
        [GeographyKey] int NULL,   
        [Speed] float NOT NULL,   
        [YearMeasured] int NOT NULL  
)  
WITH (LOCATION='/Demo/',   
        DATA_SOURCE = AzureStorage,  
        FILE_FORMAT = TextFileFormat  
);  
  
--5: Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
## <a name="polybase-queries"></a>Consultas do PolyBase  
 O PolyBase é adequado para três funções:  
  
-   consultas ad hoc em tabelas externas.  
  
-   importação de dados.  
  
-   exportação de dados.  
  
### <a name="query-examples"></a>Exemplos de consulta  
  
-   Consultas ad hoc  
  
    ```tsql  
    -- PolyBase Scenario 1: Ad-Hoc Query joining relational with Hadoop data   
    -- Select customers who drive faster than 35 mph: joining structured customer data stored   
    -- in SQL Server with car sensor data stored in Hadoop.  
    SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,   
            Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
    FROM Insured_Customers, CarSensor_Data  
    WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35   
    ORDER BY CarSensor_Data.Speed DESC  
    OPTION (FORCE EXTERNALPUSHDOWN);    -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
    ```  
  
-   Importando dados  
  
    ```tsql  
    -- PolyBase Scenario 2: Import external data into SQL Server.  
    -- Import data for fast drivers into SQL Server to do more in-depth analysis and  
    -- leverage Columnstore technology.  
  
    SELECT DISTINCT   
            Insured_Customers.FirstName, Insured_Customers.LastName,   
            Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
    INTO Fast_Customers from Insured_Customers INNER JOIN   
    (  
            SELECT * FROM CarSensor_Data where Speed > 35   
    ) AS SensorD  
    ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
    ORDER BY YearlyIncome  
  
    CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
    ```  
  
-   Exportando dados  
  
    ```  
    -- PolyBase Scenario 3: Export data from SQL Server to Hadoop.  
  
    -- Enable INSERT into external table  
    sp_configure ‘allow polybase export’, 1;  
    reconfigure  
  
    -- Create an external table.   
    CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
            [FirstName] char(25) NOT NULL,   
            [LastName] char(25) NOT NULL,   
            [YearlyIncome] float NULL,   
            [MaritalStatus] char(1) NOT NULL  
    )  
    WITH (  
            LOCATION='/old_data/2009/customerdata',  
            DATA_SOURCE = HadoopHDP2,  
            FILE_FORMAT = TextFileFormat,  
            REJECT_TYPE = VALUE,  
            REJECT_VALUE = 0  
    );  
  
    -- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
    INSERT INTO dbo.FastCustomer2009  
    SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
    ON (T1.CustomerKey = T2.CustomerKey)  
    WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
    ```  
  
## <a name="managing-polybase-objects-in-ssms"></a>Gerenciando objetos PolyBase no SSMS  
 No SSMS, as tabelas externas são exibidas em uma pasta separada **Tabelas Externas**. As fontes de dados externas e os formatos de arquivo externos estão em subpastas em **Recursos Externos**.  
  
 ![Objetos do PolyBase no SSMS](../../relational-databases/polybase/media/polybase-management.png "Objetos do PolyBase no SSMS")  
  
## <a name="troubleshooting"></a>Solução de problemas  
 Use DMVs para solucionar problemas de desempenho e consultas. Para obter detalhes, veja [Solução de problemas do PolyBase](../../relational-databases/polybase/polybase-troubleshooting.md).  
  
 Após a atualização do SQL Server 2016 RC1 para RC2 ou RC3, as consultas poderão falhar. Para obter detalhes e uma solução, veja [Notas de versão do SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md) e procure “PolyBase”.  
  
## <a name="next-steps"></a>Próximas etapas  
 Para entender o recurso de expansão, veja [Grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).  Para monitorar o PolyBase, veja [Solução de problemas do PolyBase](../../relational-databases/polybase/polybase-troubleshooting.md). Para solucionar problemas de desempenho do PolyBase, confira [Solução de problemas do PolyBase com exibições dinâmicas de gerenciamento](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80).  
  
## <a name="see-also"></a>Consulte também  
 [Guia do PolyBase](../../relational-databases/polybase/polybase-guide.md)   
 [Grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)   
 [Procedimentos armazenados do PolyBase](http://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  

