---
title: Definir configurações avançadas para arquivos de log do DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- log files,advanced settings
- dqs log files,advanced settings
ms.assetid: 1d565748-9759-425c-ae38-4d2032a86868
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6b4054be2d956bccecd1d64dc807671caf8f980f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937987"
---
# <a name="configure-advanced-settings-for-dqs-log-files"></a>Definir configurações avançadas para arquivos de log do DQS
  Este tópico descreve como definir configurações avançadas para os arquivos de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , como definir o limite de tamanho de arquivo de rolagem dos arquivos de log, definir o padrão de carimbo de data/hora dos eventos etc.  
  
> [!NOTE]  
>  Essas atividades não podem ser executadas por meio do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], e destinam-se apenas a usuários avançados.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
  
-   A conta de usuário do Windows deve ser um membro da função de servidor fixa sysadmin na instância do SQL Server para modificar as configurações na tabela A_CONFIGURATION do banco de dados DQS_MAIN.  
  
-   Você deve estar conectado como membro do grupo Administradores no computador onde está modificando o arquivo DQLog.Client.xml para definir as configurações de log do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
##  <a name="configure-data-quality-server-log-settings"></a><a name="DQSServer"></a>Definir configurações de log do servidor de qualidade de dados  
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
>  As configurações de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] são geradas e armazenadas dinamicamente no arquivo DQS_MAIN.Log, que geralmente estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log caso você tenha instalado a instância padrão do SQL Server. No entanto, as alterações feitas diretamente nesse arquivo não são mantidas, sendo substituídas pelas configurações da tabela A_CONFIGURATION no banco de dados DQS_MAIN.  
  
##  <a name="configure-data-quality-client-log-settings"></a><a name="DQSClient"></a>Definir configurações de log de Data Quality Client  
 O [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] arquivo de configuração de configuração de log, DQLog.Client.xml, normalmente está disponível em C:\Program Files\Microsoft SQL Server\120\Tools\Binn\DQ\config. O conteúdo do arquivo XML é semelhante ao arquivo XML que você modificou anteriormente para as [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] definições de configuração de log. Para configurar as configurações de log do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] :  
  
1.  Execute qualquer ferramenta de edição XML ou bloco de notas como um administrador.  
  
2.  Abra o arquivo DQLog.Client.xml na ferramenta ou no bloco de notas.  
  
3.  Faça as alterações necessárias e salve o arquivo para aplicar as novas alterações de log.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar níveis de severidade para arquivos de log do DQS](../../2014/data-quality-services/configure-severity-levels-for-dqs-log-files.md)  
  
  
