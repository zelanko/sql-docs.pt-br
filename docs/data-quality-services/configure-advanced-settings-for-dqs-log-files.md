---
title: Definir configurações avançadas para arquivos de log do DQS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log files,advanced settings
- dqs log files,advanced settings
ms.assetid: 1d565748-9759-425c-ae38-4d2032a86868
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65b187d2c5b3f829a6769cae1bc803ae5c64c383
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="configure-advanced-settings-for-dqs-log-files"></a>Definir configurações avançadas para arquivos de log do DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como definir configurações avançadas para os arquivos de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , como definir o limite de tamanho de arquivo de rolagem dos arquivos de log, definir o padrão de carimbo de data/hora dos eventos etc.  
  
> [!NOTE]  
>  Essas atividades não podem ser executadas por meio do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], e destinam-se apenas a usuários avançados.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
-   A conta de usuário do Windows deve ser um membro da função de servidor fixa sysadmin na instância do SQL Server para modificar as configurações na tabela A_CONFIGURATION do banco de dados DQS_MAIN.  
  
-   Você deve estar conectado como membro do grupo Administradores no computador onde está modificando o arquivo DQLog.Client.xml para definir as configurações de log do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
##  <a name="DQSServer"></a> Definir configurações de log do servidor do Data Quality  
 As configurações de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] estão presentes em um formato XML na coluna **VALUE** da linha **ServerLogging** na tabela A_CONFIGURATION no banco de dados DQS_MAIN. Você pode executar a seguinte consulta SQL para exibir informações de configuração:  
  
```  
select * from DQS_MAIN.dbo.A_CONFIGURATION where NAME='ServerLogging'  
```  
  
 Você deve atualizar as informações apropriadas na coluna **VALUE** da linha **ServerLogging** para alterar as configurações de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] . Neste exemplo, atualizaremos as configurações de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] para definir o limite de tamanho do arquivo de rolagem como 25000 KB (o padrão é 20000 KB).  
  
1.  Inicie o Microsoft SQL Server Management Studio e conecte-se à instância apropriada do SQL Server.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no servidor e, depois, clique em **Nova Consulta**.  
  
3.  Na janela Editor de Consultas, copie as seguintes instruções SQL:  
  
    ```  
    -- Begin the transaction.  
    BEGIN TRAN  
    GO  
    -- set the XML value field for the row with name=ServerLogging  
    update DQS_MAIN.dbo.A_CONFIGURATION   
    set VALUE='<configuration>  
      <configSections>  
        <section name="loggingConfiguration" type="Microsoft.Practices.EnterpriseLibrary.Logging.Configuration.LoggingSettings, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" />  
      </configSections>  
      <loggingConfiguration name="Logging Application Block" tracingEnabled="true" defaultCategory="" logWarningsWhenNoCategoriesMatch="true">  
        <listeners>  
          <add fileName="###REPLACE_THIS_WITH_SQL_SERVER_INSTANCE_LOG_FOLDER_NAME###DQServerLog.###REPLACE_THIS_WITH_SQL_CATALOG_NAME###.log" footer="" formatter="Custom Text Formatter" header="" rollFileExistsBehavior="Increment" rollInterval="None" rollSizeKB="25000" timeStampPattern="yyyy-MM-dd" listenerDataType="Microsoft.Practices.EnterpriseLibrary.Logging.Configuration.RollingFlatFileTraceListenerData, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" traceOutputOptions="None" filter="All" type="Microsoft.Practices.EnterpriseLibrary.Logging.TraceListeners.RollingFlatFileTraceListener, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="Rolling Flat File Trace Listener" />  
        </listeners>  
        <formatters>  
          <add template="{timestamp(local)}|[{threadName}]|{dictionary({value}|)}{message}" type="Microsoft.Practices.EnterpriseLibrary.Logging.Formatters.TextFormatter, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="Custom Text Formatter" />  
        </formatters>  
        <logFilters>  
          <add enabled="true" type="Microsoft.Practices.EnterpriseLibrary.Logging.Filters.LogEnabledFilter, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="LogEnabled Filter" />  
        </logFilters>  
        <categorySources />  
        <specialSources>  
          <allEvents switchValue="All" name="All Events" />  
          <notProcessed switchValue="All" name="Unprocessed Category" />  
          <errors switchValue="All" name="Logging Errors & Warnings">  
            <listeners>  
              <add name="Rolling Flat File Trace Listener" />  
            </listeners>  
          </errors>  
        </specialSources>  
      </loggingConfiguration>  
    </configuration>'  
    WHERE NAME='ServerLogging'  
    GO  
    -- check the result  
    select * from DQS_MAIN.dbo.A_CONFIGURATION where NAME='ServerLogging'  
  
    -- Commit the transaction.  
    COMMIT TRAN  
  
    ```  
  
4.  Pressione F5 para executar as instruções. Consulte o painel **Resultados** para verificar se as instruções foram executadas com êxito.  
  
5.  Para aplicar as alterações feitas na configuração de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , execute as seguintes instruções Transact-SQL. Abra uma nova janela Editor de Consultas e cole as seguintes instruções Transact-SQL:  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    DECLARE @return_value int  
    EXEC @return_value = [internal_core].[RefreshLogSettings]  
    SELECT 'Return Value' = @return_value  
    GO  
  
    ```  
  
6.  Pressione F5 para executar as instruções. Consulte o painel **Resultados** para verificar se as instruções foram executadas com êxito.  
  
> [!NOTE]  
>  As configurações de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] são geradas e armazenadas dinamicamente no arquivo DQS_MAIN.Log, que geralmente estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log caso você tenha instalado a instância padrão do SQL Server. No entanto, as alterações feitas diretamente nesse arquivo não são mantidas, sendo substituídas pelas configurações da tabela A_CONFIGURATION no banco de dados DQS_MAIN.  
  
##  <a name="DQSClient"></a> Definir configurações de log do cliente do Data Quality  
 O arquivo de configuração de log do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , DQLog.Client.xml, geralmente está disponível em C:\Arquivos de Programas\Microsoft SQL Server\130\Tools\Binn\DQ\config. O conteúdo do arquivo XML é semelhante ao arquivo XML cujas configurações de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] você modificou anteriormente. Para configurar as configurações de log do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] :  
  
1.  Execute qualquer ferramenta de edição XML ou bloco de notas como um administrador.  
  
2.  Abra o arquivo DQLog.Client.xml na ferramenta ou no bloco de notas.  
  
3.  Faça as alterações necessárias e salve o arquivo para aplicar as novas alterações de log.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar níveis de severidade para arquivos de log do DQS](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)  
  
  
