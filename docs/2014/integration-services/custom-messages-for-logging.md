---
title: Custom Messages for Logging | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], custom
- writing log entries
- SSIS packages, logs
- custom messages for logging [Integration Services]
ms.assetid: 3c74bba9-02b7-4bf5-bad5-19278b680730
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c479c8e7026e549c33b838c39017c9063894b607
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828773"
---
# <a name="custom-messages-for-logging"></a>Mensagens personalizadas para log
  O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece um rico conjunto de eventos personalizados para gravação de entradas de log para pacotes e diversas tarefas. Você pode usar essas entradas para salvar informações detalhadas sobre progresso de execução, resultados e problemas registrando eventos predefinidos ou mensagens definidas pelo usuário para análise posterior. Por exemplo, você pode registrar quando uma inserção em massa é iniciada ou finalizada para identificar problemas de desempenho na execução do pacote.  
  
 As entradas de log personalizadas são um conjunto de entradas diferente do conjunto de eventos de log padrão, disponível para pacotes e todos os contêineres e tarefas. As entradas de log personalizadas são elaboradas para capturar informações úteis sobre uma tarefa específica em um pacote. Por exemplo, uma das entradas de log personalizadas da tarefa Executar SQL registra a instrução SQL executada pela tarefa no log.  
  
 Todas as entradas de log incluem informações de data e hora, inclusive as entradas de log que são gravadas automaticamente quando um pacote é iniciado ou finalizado. Diversos tipos de eventos de log gravam várias entradas no log. Isso acontece normalmente quando o evento tem fases diferentes. Por exemplo, o evento de log `ExecuteSQLExecutingQuery` grava três entradas: uma entrada depois que a tarefa adquire uma conexão com o banco de dados, outra depois que a tarefa começa a preparar a instrução SQL e uma depois que a execução da instrução SQL foi concluída.  
  
 Os objetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a seguir têm entradas de log personalizadas:  
  
 [Pacote](#Package)  
  
 [Tarefa Inserção em Massa](#BulkInsert)  
  
 [Tarefa de Fluxo de Dados](#DataFlow)  
  
 [Tarefa Executar DTS 2000](#ExecuteDTS200)  
  
 [Tarefa Executar Processo](#ExecuteProcess)  
  
 [Tarefa Executar SQL](#ExecuteSQL)  
  
 [Tarefa Sistema de Arquivos](#FileSystem)  
  
 [Tarefa FTP](#FTP)  
  
 [Tarefa Fila de Mensagens](#MessageQueue)  
  
 [Tarefa Script](#Script)  
  
 [Tarefa Enviar Email](#SendMail)  
  
 [Tarefa Transferir Banco de Dados](#TransferDatabase)  
  
 [Tarefa Transferir Mensagens de Erro](#TransferErrorMessages)  
  
 [Tarefa Transferir Trabalhos](#TransferJobs)  
  
 [Tarefa Transferir Logons](#TransferLogins)  
  
 [Tarefa Transferir Procedimentos Armazenados Mestres](#TransferMasterStoredProcedures)  
  
 [Tarefa Transferir Objetos do SQL Server](#TransferSQLServerObjects)  
  
 [Tarefa Serviços Web](#WebServices)  
  
 [Tarefa Leitor de Dados do WMI](#WMIDataReader)  
  
 [Tarefa Detector de Eventos do WMI](#WMIEventWatcher)  
  
 [XML Task](#XML)  
  
## <a name="log-entries"></a>Entradas de log  
  
###  <a name="Package"></a> Pacote  
 A tabela a seguir relaciona as entradas de log personalizadas para pacotes.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`PackageStart`|Indica que o pacote começou a ser executado.<br /><br /> Observação: Esta entrada de log é gravada no log automaticamente. Não é possível excluí-la.|  
|`PackageEnd`|Indica que o pacote foi concluído.<br /><br /> Observação: Esta entrada de log é gravada no log automaticamente. Não é possível excluí-la.|  
|`Diagnostic`|Fornece informações sobre a configuração do sistema que afeta a execução de pacotes como os executáveis numéricos que podem ser executados simultaneamente.<br /><br /> A entrada de log `Diagnostic` também inclui entradas anteriores e posteriores a chamadas para provedores de dados externos. Para obter mais informações, consulte [Solução de problemas de conectividade de pacotes de ferramentas](troubleshooting/troubleshooting-tools-for-package-connectivity.md).|  
  
###  <a name="BulkInsert"></a> Tarefa Inserção em Massa  
 A seguinte tabela relaciona as entradas de log personalizadas para a tarefa inserção em massa .  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`DTSBulkInsertTaskBegin`|Indica que a inserção em massa iniciou.|  
|`DTSBulkInsertTaskEnd`|Indica que a inserção em massa foi concluída.|  
|`DTSBulkInsertTaskInfos`|Fornece informações descritivas sobre a tarefa.|  
  
###  <a name="DataFlow"></a> Tarefa de Fluxo de Dados  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa de Fluxo de Dados.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`BufferSizeTuning`|Indica que a tarefa de Fluxo de Dados alterou o tamanho do buffer. A entrada de log descreve os motivos da mudança de tamanho e relaciona o novo tamanho do buffer temporário.|  
|`OnPipelinePostEndOfRowset`|Indica que um componente recebeu o sinal de final do conjunto de linhas, definido pela última chamada do método `ProcessInput`. Uma entrada é gravada para cada componente no fluxo de dados que processa a entrada. A entrada contém o nome do componente.|  
|`OnPipelinePostPrimeOutput`|Indica que o componente completou sua última chamada para o método `PrimeOutput`. Dependendo do fluxo de dados, várias entradas de log podem ser gravadas. Se o componente for uma fonte, isto significará que o componente tem linhas de processamento concluídas.|  
|`OnPipelinePreEndOfRowset`|Indica que um componente está prestes a receber o sinal de final do conjunto de linhas, definido pela última chamada do método `ProcessInput`. Uma entrada é gravada para cada componente no fluxo de dados que processa a entrada. A entrada contém o nome do componente.|  
|`OnPipelinePrePrimeOutput`|Indica que o componente está prestes a receber sua chamada a partir do método `PrimeOutput`. Dependendo do fluxo de dados, várias entradas de log podem ser gravadas.|  
|`OnPipelineRowsSent`|Informa o número de linhas fornecido a uma entrada de componente por uma chamada para o método `ProcessInput`. A entrada de log inclui o nome do componente.|  
|`PipelineBufferLeak`|Fornece informações sobre qualquer componente que manteve buffers ativos depois que o gerenciador de buffers for desativado. Isso significa que os recursos de buffers não foram liberados e pode haver vazamentos de memória. A entrada de log fornece o nome do componente e a ID do buffer.|  
|`PipelineExecutionPlan`|Informa o plano de execução do fluxo de dados. Fornece informações sobre como os buffers serão enviados a componentes. Essas informações, em combinação com a entrada de PipelineExecutionTrees, descrevem o que está acontecendo na tarefa.|  
|`PipelineExecutionTrees`|Informa as árvores de execução sobre o layout do fluxo de dados. O agendador do mecanismo de fluxo de dados usa as árvores para compilar o plano de execução do fluxo de dados.|  
|`PipelineInitialization`|Fornece informações de inicialização sobre a tarefa. Essas informações incluem os diretórios para armazenamento temporário de dados de BLOB, o tamanho do buffer padrão e o número de linhas em um buffer. Dependendo da configuração da tarefa de Fluxo de Dados, várias entradas de log podem ser gravadas.|  
  
###  <a name="ExecuteDTS200"></a> Tarefa Executar DTS 2000  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Executar DTS 2000.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`ExecuteDTS80PackageTaskBegin`|Indica que a tarefa começou a ser executada em um pacote DTS 2000.|  
|`ExecuteDTS80PackageTaskEnd`|Indica que a tarefa foi concluída.<br /><br /> Observação: O pacote DTS 2000 pode continuar a executar após a conclusão da tarefa.|  
|`ExecuteDTS80PackageTaskTaskInfo`|Fornece informações descritivas sobre a tarefa.|  
|`ExecuteDTS80PackageTaskTaskResult`|Informa o resultado de execução do pacote DTS 2000 executado pela tarefa.|  
  
###  <a name="ExecuteProcess"></a> Tarefa Executar Processo  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Executar Processo.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|Fornece informações sobre o processo do executável que a tarefa está configurada para executar.<br /><br /> São gravadas duas entradas de log. Uma contém informações sobre o nome e o local do executável que a tarefa executa e o outro registra a saída do executável.|  
|`ExecuteProcessVariableRouting`|Fornece informações sobre quais variáveis são encaminhadas para a entrada e as saídas do executável. As entradas de log são gravadas em stdin (a entrada), stdout (a saída) e stderr (a saída do erro).|  
  
###  <a name="ExecuteSQL"></a> Tarefa Executar SQL  
 A tabela a seguir descreve a entrada de log personalizada da tarefa Executar SQL.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|Fornece informações sobre as fases de execução da instrução SQL. As entradas de log são gravadas quando a tarefa adquire conexão com o banco de dados, quando a tarefa começa a preparar a instrução SQL e depois que a execução da instrução SQL é concluída. A entrada de log da fase de preparação inclui a instrução SQL usada pela tarefa.|  
  
###  <a name="FileSystem"></a> Tarefa Sistema de Arquivos  
 A tabela a seguir descreve a entrada de log personalizada da tarefa Sistema de Arquivos.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`FileSystemOperation`|Informa a operação executada pela tarefa. A entrada de log é gravada quando a operação de sistema de arquivos é iniciada e inclui informações sobre a origem e o destino.|  
  
###  <a name="FTP"></a> Tarefa FTP  
 A tabela a seguir relaciona as entradas de log personalizadas da tarefa FTP.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`FTPConnectingToServer`|Indica que a tarefa iniciou uma conexão com o servidor FTP.|  
|`FTPOperation`|Informa o início e o tipo de operação de FTP que a tarefa executa.|  
  
###  <a name="MessageQueue"></a> Tarefa Fila de Mensagens  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Fila de Mensagens.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`MSMQAfterOpen`|Indica que a tarefa finalizou a abertura da fila de mensagens.|  
|`MSMQBeforeOpen`|Indica que a tarefa começou a abrir a fila de mensagens.|  
|`MSMQBeginReceive`|Indica que a tarefa começou a receber uma mensagem.|  
|`MSMQBeginSend`|Indica que a tarefa começou a enviar uma mensagem.|  
|`MSMQEndReceive`|Indica que a tarefa terminou de receber uma mensagem.|  
|`MSMQEndSend`|Indica que a tarefa terminou de enviar uma mensagem|  
|`MSMQTaskInfo`|Fornece informações descritivas sobre a tarefa.|  
|`MSMQTaskTimeOut`|Indica que o tempo limite da tarefa foi esgotado.|  
  
###  <a name="Script"></a> Tarefa Script  
 A tabela a seguir descreve a entrada de log personalizada da tarefa Script.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`ScriptTaskLogEntry`|Informa os resultados da implementação do registro em log no script. Uma entrada de log é gravada para cada chamada ao método `Log` do objeto `Dts`. A entrada é gravada quando o código é executado. Para obter mais informações, consulte [Registro em log na Tarefa Script](extending-packages-scripting/task/logging-in-the-script-task.md).|  
  
###  <a name="SendMail"></a> Tarefa Enviar Email  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Enviar Email.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`SendMailTaskBegin`|Indica que a tarefa começou a enviar uma mensagem de email.|  
|`SendMailTaskEnd`|Indica que a tarefa terminou de enviar uma mensagem de email.|  
|`SendMailTaskInfo`|Fornece informações descritivas sobre a tarefa.|  
  
###  <a name="TransferDatabase"></a> Tarefa Transferir Banco de Dados  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Transferir Banco de Dados.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`SourceDB`|Especifica o banco de dados que a tarefa copiou.|  
|`SourceSQLServer`|Especifica o computador a partir do qual o banco de dados foi copiado.|  
  
###  <a name="TransferErrorMessages"></a> Tarefa Transferir Mensagens de Erro  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Transferir Mensagens de Erro.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`TransferErrorMessagesTaskFinishedTransferringObjects`|Indica que a tarefa terminou de transferir mensagens de erro.|  
|`TransferErrorMessagesTaskStartTransferringObjects`|Indica que a tarefa começou a transferir as mensagens de erro.|  
  
###  <a name="TransferJobs"></a> Tarefa Transferir Trabalhos  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Transferir Trabalhos.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`TransferJobsTaskFinishedTransferringObjects`|Indica que a tarefa terminou a transferência dos trabalhos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent.|  
|`TransferJobsTaskStartTransferringObjects`|Indica que a tarefa começou a transferência dos trabalhos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent.|  
  
###  <a name="TransferLogins"></a> Tarefa Transferir Logons  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Transferir Logons.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`TransferLoginsTaskFinishedTransferringObjects`|Indica que a tarefa terminou a transferência dos logons.|  
|`TransferLoginsTaskStartTransferringObjects`|Indica que a tarefa começou a transferência dos logons.|  
  
###  <a name="TransferMasterStoredProcedures"></a> Tarefa Transferir Procedimentos Armazenados Mestres  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Transferir Procedimentos Armazenados Mestres.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`TransferStoredProceduresTaskFinishedTransferringObjects`|Indica que a tarefa terminou de transferir procedimentos armazenados definidos pelo usuário armazenados no banco de dados **mestre** .|  
|`TransferStoredProceduresTaskStartTransferringObjects`|Indica que a tarefa começou a transferir procedimentos armazenados definidos pelo usuário armazenados no banco de dados **mestre** .|  
  
###  <a name="TransferSQLServerObjects"></a> Tarefa Transferir Objetos do SQL Server  
 A tabela a seguir relaciona as entradas de log personalizadas da tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`TransferSqlServerObjectsTaskFinishedTransferringObjects`|Indica que a tarefa terminou a transferência dos objetos de banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|`TransferSqlServerObjectsTaskStartTransferringObjects`|Indica que a tarefa começou a transferência dos objetos de banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
  
###  <a name="WebServices"></a> Tarefa Serviços Web  
 A tabela a seguir relaciona as entradas de log personalizadas que podem ser habilitadas para a tarefa Serviços Web.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`WSTaskBegin`|A tarefa começou a acessar um serviço Web.|  
|`WSTaskEnd`|A tarefa completou um método de serviço Web.|  
|`WSTaskInfo`|Informações descritivas sobre a tarefa.|  
  
###  <a name="WMIDataReader"></a> Tarefa Leitor de Dados do WMI  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Leitor de Dados do WMI.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|Indica que a tarefa começou a ser ler os dados do WMI.|  
|`WMIDataReaderOperation`|Informa a consulta WQL executada pela tarefa.|  
  
###  <a name="WMIEventWatcher"></a> Tarefa Detector de Eventos do WMI  
 A tabela a seguir relaciona as entradas de registro personalizadas da tarefa Detector de Eventos do WMI.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|Mostra que o evento ocorrido era o que a tarefa estava monitorando.|  
|`WMIEventWatcherTimedout`|Indica que o tempo limite da tarefa foi esgotado.|  
|`WMIEventWatcherWatchingForWMIEvents`|Indica que a tarefa começou a executar a consulta WQL. A entrada inclui a consulta.|  
  
###  <a name="XML"></a> XML Task  
 A tabela a seguir descreve a entrada de log personalizada da tarefa XML.  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`XMLOperation`|Fornece informações sobre a operação executada pela tarefa|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog [Logging custom events for Integration Services tasks](https://go.microsoft.com/fwlink/?LinkId=150580) (Registrando eventos personalizados para tarefas do Integration Services), em dougbert.com.  
  
## <a name="see-also"></a>Consulte também  
 [Registro em Log do Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
  
