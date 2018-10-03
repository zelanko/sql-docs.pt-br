---
title: Constantes enumeradas em expressões de propriedade | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], expressions
- dynamic properties
- updating package properties
- enumerated constants [Integration Services]
- property expressions [Integration Services]
ms.assetid: a4418315-38e2-4ad3-8784-576163b25d6f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb882f13b7f4fd19cab5f9b44885647aaafa65d3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089640"
---
# <a name="enumerated-constants-in-property-expressions"></a>Constantes enumeradas em expressões de propriedade
  Se as expressões de propriedade incluírem valores de uma lista de membros de enumerador, a expressão deverá usar o valor numérico do membro de enumerador em vez do nome amigável do membro. Por exemplo, se uma expressão define o `LoggingMode` propriedade, use o valor numérico 2 em vez do nome amigável desabilitada.  
  
 Este tópico relaciona apenas os valores numéricos equivalentes a nomes amigáveis de enumeradores cujos membros são usados normalmente em expressões de propriedade. O modelo de objeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui muitos enumeradores adicionais que podem ser usados quando você programa o modelo de objeto para criar pacotes programaticamente ou codifica elementos personalizados de pacote como tarefas e componentes de fluxo de dados.  
  
 Além das propriedades personalizadas para pacotes e objetos de pacote, a janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] inclui um conjunto de propriedades disponíveis para pacotes, tarefas e os contêineres Loop Foreach, Loop For e Sequência. As propriedades comuns definidas pelos valores de enumeradores `ForceExecutionResult`, `LoggingMode`, `IsolationLevel`e `Transaction Option` são relacionadas na seção Propriedades comuns.  
  
 As seções a seguir fornecem informações sobre constantes enumeradas:  
  
 [Pacote](#Package)  
  
 [Enumeradores de Loop Foreach](#Foreach)  
  
 [Tarefas](#Tasks)  
  
 [Tarefas do Plano de Manutenção](#MaintenancePlanTasks)  
  
 [Propriedades comuns](#CommonProperties)  
  
##  <a name="Package"></a> Pacote  
 As tabelas a seguir relacionam os nomes amigáveis e os equivalentes em valor numérico para propriedades de pacotes definidas por você usando valores de um enumerador.  
  
 `PackageType` propriedade — definida usando valores da `DTSPackageType` enumeração.  
  
|Nome amigável em DTSPackageType|Valor numérico|  
|-------------------------------------|-------------------|  
|Default|0|  
|DTSWizard|1|  
|DTSDesigner|2|  
|SQLReplication|3|  
|DTSDesigner100|5|  
|SQLDBMaint|6|  
  
 `CheckpointUsage` propriedade — definida usando valores da `DTSCheckpointUsage` enumeração.  
  
|Nome amigável em DTSCheckpointUsage|Valor numérico|  
|-----------------------------------------|-------------------|  
|Never|0|  
|IfExists|1|  
|Always|2|  
  
 `PackagePriorityClass` propriedade — definida usando valores da `DTSPriorityClass` enumeração.  
  
|Nome amigável em DTSPriorityClass|Valor numérico|  
|---------------------------------------|-------------------|  
|Default|0|  
|AboveNormal|1|  
|Normal|2|  
|BelowNormal|3|  
|Idle|4|  
  
 `ProtectionLevel` propriedade — definida usando valores da `DTSProtectionLevel` enumeração.  
  
|Nome amigável em DTSProtectionLevel|Valor numérico|  
|-----------------------------------------|-------------------|  
|DontSaveSensitive|0|  
|EncryptSensitiveWithUserKey|1|  
|EncryptSensitiveWithPassword|2|  
|EncryptAllWithPassword|3|  
|EncryptAllWithUserKey|4|  
|ServerStorage|5|  
  
##  <a name="PrecedenceConstraints"></a> Restrições de precedência  
 `EvalOp` propriedade — definida usando valores da `DTSPrecedenceEvalOp` enumeração.  
  
|Nome amigável em DTSPrecedenceEvalOp|Valor numérico|  
|------------------------------------------|-------------------|  
|Expression|1|  
|Constraint|2|  
|ExpressionAndConstraint|3|  
|ExpressionOrConstraint|4|  
  
 `Value` propriedade — definida usando valores da `DTSExecResult` enumeração.  
  
|Nome amigável|Valor numérico|  
|-------------------|-------------------|  
|Êxito|0|  
|Failure|1|  
|Completion|2|  
|Canceled|3|  
  
##  <a name="Foreach"></a> Enumeradores de Loop Foreach  
 O Loop Foreach inclui um conjunto de enumeradores com propriedades que podem ser definidas por expressões de propriedade.  
  
### <a name="foreach-ado-enumerator"></a>Enumerador ADO Foreach  
 `Type` propriedade — definida usando valores da `ADOEnumerationType` enumeração.  
  
|Nome amigável em ADOEnumerationType|Valor numérico|  
|-----------------------------------------|-------------------|  
|EnumerateTables|0|  
|EnumerateAllRows|1|  
|EnumerateRowsInFirstTable|2|  
  
### <a name="foreach-nodelist-enumerator"></a>Enumerador Nodelist Foreach  
 `SourceDocumentType`, `InnerXPathStringSourceType`, e **OuterXPathStringSourceType** propriedades — definida usando valores da `SourceType` enumeração.  
  
|Nome amigável em SourceType|Valor numérico|  
|---------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
|DirectInput|2|  
  
 `EnumerationType` propriedade — definida usando valores da `EnumerationType` enumeração.  
  
|Nome amigável em EnumerationType|Valor numérico|  
|--------------------------------------|-------------------|  
|Navigator|0|  
|Nó|1|  
|NodeText|2|  
|ElementCollection|3|  
  
 `InnerElementType` propriedade — definida usando valores da `InnerElementType` enumeração.  
  
|Nome amigável em InnerElementType|Valor numérico|  
|---------------------------------------|-------------------|  
|Navigator|0|  
|Nó|1|  
|NodeText|2|  
  
##  <a name="Tasks"></a> Tarefas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui várias tarefas com propriedades que podem ser definidas por expressões de propriedade.  
  
### <a name="analysis-services-execute-ddl-task"></a>Tarefa Executar DDL do Analysis Services  
 `SourceType` propriedade — definida usando valores da `DDLSourceType` enumeração.  
  
|Nome amigável em DDLSourceType|Valor numérico|  
|------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variável|2|  
  
### <a name="bulk-insert-task"></a>Tarefa Inserção em Massa  
 `DataFileType` propriedade — definida usando valores da `DTSBulkInsert_DataFileType` enumeração.  
  
|Nome amigável em DTSBulkInsert_DataFileType|Valor numérico|  
|--------------------------------------------------|-------------------|  
|DTSBulkInsert_DataFileType_Char|0|  
|DTSBulkInsert_DataFileType_Native|1|  
|DTSBulkInsert_DataFileType_WideChar|2|  
|DTSBulkInsert_DataFileType_WideNative|3|  
  
### <a name="execute-sql-task"></a>Tarefa Executar SQL  
 `ResultSetType` propriedade — definida usando valores da `ResultSetType` enumeração.  
  
|Nome amigável em ResultSetType|Valor numérico|  
|------------------------------------|-------------------|  
|ResultSetType_None|1|  
|ResultSetType_SingleRow|2|  
|ResultSetType_Rowset|3|  
|ResultSetType_XML|4|  
  
 `SqlStatementSourceType` propriedade — definida usando valores da `SqlStatementSourceType` enumeração.  
  
|Nome amigável em SqlStatementSourceType|Valor numérico|  
|---------------------------------------------|-------------------|  
|DirectInput|1|  
|FileConnection|2|  
|Variável|3|  
  
### <a name="file-system-task"></a>Tarefa Sistema de Arquivos  
 `Operation` propriedade — definida usando valores da `DTSFileSystemOperation` enumeração.  
  
|Nome amigável em DTSFileSystemOperation|Valor numérico|  
|---------------------------------------------|-------------------|  
|CopyFile|0|  
|MoveFile|1|  
|DeleteFile|2|  
|RenameFile|3|  
|SetAttributes|4|  
|CreateDirectory|5|  
|CopyDirectory|6|  
|MoveDirectory|7|  
|DeleteDirectory|8|  
|DeleteDirectoryContent|9|  
  
 `Attributes` propriedade — definida usando valores da `DTSFileSystemAttributes` enumeração.  
  
|Nome amigável em DTSFileSystemAttributes|Valor numérico|  
|----------------------------------------------|-------------------|  
|Normal|0|  
|Archive|1|  
|Hidden|2|  
|ReadOnly (somente-leitura)|4|  
|Sistema|8|  
  
### <a name="ftp-task"></a>Tarefa FTP  
 `Operation` propriedade — definida usando valores da `DTSFTPOp` enumeração.  
  
|Nome amigável em DTSFTPOp|Valor numérico|  
|-------------------------------|-------------------|  
|Send|0|  
|Receive (receber)|1|  
|DeleteLocal|2|  
|DeleteRemote|3|  
|MakeDirLocal|4|  
|MakeDirRemote|5|  
|RemoveDirLocal|6|  
|RemoveDirRemote|7|  
  
### <a name="message-queue-task"></a>Message Queue Task  
 `MessageType` propriedade — definida usando valores da `MQMessageType` enumeração.  
  
|Nome amigável em MQMessageType|Valor numérico|  
|------------------------------------|-------------------|  
|DTSMQMessageType_String|0|  
|DTSMQMessageType_DataFile|1|  
|DTSMQMessageType_Variables|2|  
|DTSMQMessagType_StringMessageToVariable|3|  
  
 `StringCompareType` propriedade — definida usando valores da `MQStringMessageCompare` enumeração.  
  
|Nome amigável em MQStringMessageCompare|Valor numérico|  
|---------------------------------------------|-------------------|  
|DTSMQStringMessageCompare_None|0|  
|DTSMQStringMessageCompare_Exact|1|  
|DTSMQStringMessageCompare_IgnoreCase|2|  
|DTSMQStringMessageCompare_Contains|3|  
  
 `TaskType` propriedade — definida usando valores da `MQType` enumeração.  
  
|Nome amigável em MQType|Valor numérico|  
|-----------------------------|-------------------|  
|DTSMQType_Sender|0|  
|DTSMQType_Receiver|1|  
  
### <a name="send-mail-task"></a>Tarefa Enviar Email  
 `MessageSourceType` propriedade — definida usando valores da `SendMailMessageSourceType` enumeração.  
  
|Nome amigável em SendMailMessageSourceType|Valor numérico|  
|------------------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variável|2|  
  
 `Priority` propriedade — definida usando valores da `MailPriority` enumeração.  
  
|Nome amigável em MailPriority|Valor numérico|  
|-----------------------------------|-------------------|  
|Alta|1|  
|Normal|3|  
|Baixa|5|  
  
### <a name="transfer-database-task"></a>Tarefa Transferir Banco de Dados  
 `Action` propriedade — definida usando valores da `TransferAction` enumeração.  
  
|Nome amigável em TransferAction|Valor numérico|  
|-------------------------------------|-------------------|  
|Copiar|0|  
|Mover|1|  
  
 `Method` propriedade — definida usando valores da `TransferMethod` enumeração.  
  
|Nome amigável em TransferMethod|Valor numérico|  
|-------------------------------------|-------------------|  
|DatabaseOffline|0|  
|DatabaseOnline|1|  
  
### <a name="transfer-error-messages-task"></a>Tarefa Transferir Mensagens de Erro  
 `IfObjectExists` propriedade — definida usando valores da `IfObjectExists` enumeração.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-jobs-task"></a>Tarefa Transferir Trabalhos  
 `IfObjectExists` propriedade — definida usando valores da `IfObjectExists` enumeração.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-logins-task"></a>Tarefa Transferir Logons  
 `IfObjectExists` propriedade — definida usando valores da `IfObjectExists` enumeração.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
 `LoginsToTransfer` propriedade — definida usando valores da `LoginsToTransfer` enumeração.  
  
|Nome amigável em LoginsToTransfer|Valor numérico|  
|---------------------------------------|-------------------|  
|AllLogins|0|  
|SelectedLogins|1|  
|AllLoginsFromSelectedDatabases|2|  
  
### <a name="transfer-master-stored-procedures-task"></a>Tarefa Transferir Procedimentos Armazenados Mestres  
 `IfObjectExists` propriedade — definida usando valores da `IfObjectExists` enumeração.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-sql-server-objects-task"></a>Tarefa Transferir Objetos do SQL Server  
 `ExistingData` propriedade — definida usando valores da `ExistingData` enumeração.  
  
|Nome amigável em ExistingData|Valor numérico|  
|-----------------------------------|-------------------|  
|Substituir|0|  
|Acrescentar|1|  
  
### <a name="web-service-task"></a>Tarefa Serviços Web  
 `OutputType` propriedade — definida usando valores da `DTSOutputType` enumeração.  
  
|Nome amigável em DTSOutputType|Valor numérico|  
|------------------------------------|-------------------|  
|Arquivo|0|  
|Variável|1|  
  
### <a name="wmi-data-reader-task"></a>Tarefa Leitor de Dados do WMI  
 `OverwriteDestination` propriedade — definida usando valores da `OverwriteDestination` enumeração.  
  
|Nome amigável em OverwriteDestination|Valor numérico|  
|-------------------------------------------|-------------------|  
|OverwriteDestination|0|  
|AppendToDestination|1|  
|KeepOriginal|2|  
  
 `OutputType` propriedade — definida usando valores da `OutputType` enumeração.  
  
|Nome amigável em OutputType|Valor numérico|  
|---------------------------------|-------------------|  
|DataTable|0|  
|PropertyValue|1|  
|PropertyNameAndValue|2|  
  
 `DestinationType` propriedade — definida usando valores da `DestinationType` enumeração.  
  
|Nome amigável em DestinationType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
  
 `WqlQuerySourceType` propriedade — definida usando valores da `QuerySourceType` enumeração.  
  
|Nome amigável em QuerySourceType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variável|2|  
  
 Propriedade `ActionAtEvent` do Detector de Eventos do WMI — Definida com o uso de valores da enumeração `ActionAtEvent`.  
  
|Nome amigável em ActionAtEvent|Valor numérico|  
|------------------------------------|-------------------|  
|LogTheEventAndFireDTSEvent|0|  
|LogTheEvent|1|  
  
 `ActionAtTimeout` propriedade — definida usando valores da `ActionAtTimeout` enumeração.  
  
|Nome amigável em ActionAtTimeout|Valor numérico|  
|--------------------------------------|-------------------|  
|LogTimeoutAndFireDTSEvent|0|  
|LogTimeout|1|  
  
 `AfterEvent` propriedade — definida usando valores da `AfterEvent` enumeração.  
  
|Nome amigável em AfterEvent|Valor numérico|  
|---------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 `AfterTimeout` propriedade — definida usando valores da `AfterTimeout` enumeração.  
  
|Nome amigável em AfterTimeout|Valor numérico|  
|-----------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 `WqlQuerySourceType` propriedade — definida usando valores da `QuerySourceType` enumeração.  
  
|Nome amigável em QuerySourceType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variável|2|  
  
### <a name="xml-task"></a>XML Task  
 `OperationType` propriedade — definida usando valores da `DTSXMLOperation` enumeração.  
  
|Nome amigável em DTSXMLOperation|Valor numérico|  
|--------------------------------------|-------------------|  
|Validar|0|  
|XSLT|1|  
|XPATH|2|  
|Mesclagem|3|  
|Diff|4|  
|Patch|5|  
  
 Propriedades `SourceType`, `SecondOperandType` e `XPathSourceType` — Definidas com o uso de valores da enumeração `DTSXMLSourceType`.  
  
|Nome amigável em DTSXMLSourceType|Valor numérico|  
|---------------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
|DirectInput|2|  
  
 `DestinationType` e **DiffGramDestinationType** propriedades — definida usando valores da `DTSXMLSaveResultTo` enumeração.  
  
|Nome amigável em DTSXMLSaveResultTo|Valor numérico|  
|-----------------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
  
 `ValidationType` propriedade — definida usando valores da `DTSXMLValidationType` enumeração.  
  
|Nome amigável em DTSXMLValidationType|Valor numérico|  
|-------------------------------------------|-------------------|  
|DTD|0|  
|XSD|1|  
  
 `XPathOperation` propriedade — definida usando valores da `DTSXMLXPathOperation` enumeração.  
  
|Nome amigável em DTSXMLXPathOperation|Valor numérico|  
|-------------------------------------------|-------------------|  
|Evaluation|0|  
|Valores|1|  
|NodeList|2|  
  
 `DiffOptions` propriedade — definida usando valores da `DTSXMLDiffOptions` enumeração. As opções deste enumerador não são mutuamente exclusivas. Para usar várias opções, forneça uma lista separada por vírgulas das opções a serem aplicadas.  
  
|Nome amigável em DTSXMLDiffOptions|Valor numérico|  
|----------------------------------------|-------------------|  
|None|0|  
|IgnoreChildOrder|1|  
|IgnoreComments|2|  
|IgnorePI|4|  
|IgnoreWhitespace|8|  
|IgnoreNamespaces|16|  
|IgnorePrefixes|32|  
|IgnoreXmlDecl|64|  
|IgnoreDtd|128|  
  
 `DiffAlgorithm` propriedade — definida usando valores da `DTSXMLDiffAlgorithm` enumeração.  
  
|Nome amigável em DTSXMLDiffAlgorithm|Valor numérico|  
|------------------------------------------|-------------------|  
|Auto|0|  
|Rápido|1|  
|Preciso|2|  
  
##  <a name="MaintenancePlanTasks"></a> Tarefas do Plano de Manutenção  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui um conjunto de tarefas que executam tarefas do SQL Server para uso em planos de manutenção e pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte ao trabalho programático com essas tarefas e a documentação de referência de programação não inclui documentação da API dessas tarefas e seus enumeradores.  
  
### <a name="all-maintenance-tasks"></a>Todas as Tarefas de Manutenção  
 Todas as tarefas de manutenção usam as enumerações a seguir para definir as propriedades especificadas.  
  
 `DatabaseSelectionType` propriedade — definida usando valores da `DatabaseSelection` enumeração.  
  
|Nome amigável em DatabaseSelection|Valor numérico|  
|----------------------------------------|-------------------|  
|None|0|  
|Todos|1|  
|Sistema|2|  
|Usuário|3|  
|Specific|4|  
  
 `TableSelectionType` propriedade — definida usando valores da `TableSelection` enumeração.  
  
|Nome amigável em TableSelection|Valor numérico|  
|-------------------------------------|-------------------|  
|None|0|  
|Todos|1|  
|Specific|2|  
  
 `ObjectTypeSelection` propriedade — definida usando valores da `ObjectType` enumeração.  
  
|Nome amigável em ObjectType|Valor numérico|  
|---------------------------------|-------------------|  
|Table|0|  
|Exibição|1|  
|TableView|2|  
  
### <a name="back-up-database-task"></a>Tarefa de Backup de Banco de Dados  
 `DestinationCreationType` propriedade — definida usando valores da `DestinationType` enumeração.  
  
|Nome amigável em DestinationType|Valor numérico|  
|--------------------------------------|-------------------|  
|Auto|0|  
|Manual|1|  
  
 `ExistingBackupsAction` propriedade — definida usando valores da `ActionForExistingBackups` enumeração.  
  
|Nome amigável em ActionForExistingBackups|Valor numérico|  
|-----------------------------------------------|-------------------|  
|Acrescentar|0|  
|Overwrite|1|  
  
 `BackupAction` propriedade — definida usando valores da `BackupTaskType` enumeração. Esta propriedade trabalha com o `BackupIsIncremental` propriedade para definir o tipo de backup que executa a tarefa.  
  
|Nome amigável em BackupTaskType|Valor numérico|  
|-------------------------------------|-------------------|  
|banco de dados|0|  
|Arquivos|1|  
|Log|2|  
  
 Propriedade `BackupDevice` — Definida pelo uso de valores da enumeração [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) `DeviceType`.  
  
|Nome amigável em DeviceType|Valor numérico|  
|---------------------------------|-------------------|  
|LogicalDevice|0|  
|Tape|1|  
|Arquivo|2|  
|Pipe|3|  
|VirtualDevice|4|  
  
### <a name="maintenance-cleanup-task"></a>Tarefa Limpeza de Manutenção  
 `FileTypeSelected` propriedade — definida usando valores da `FileType` enumeração.  
  
|Nome amigável em FileType|Valor numérico|  
|-------------------------------|-------------------|  
|FileBackup|0|  
|FileReport|1|  
  
 `OlderThanTimeUnitType` propriedade — definida usando valores da `TimeUnitType` enumeração.  
  
|Nome amigável em TimeUnitType|Valor numérico|  
|-----------------------------------|-------------------|  
|Day|0|  
|Week|1|  
|Month|2|  
|Year|3|  
  
### <a name="update-statistics-task"></a>Tarefa Atualizar Estatísticas  
 Propriedade `UpdateType` — Definida pelo uso de valores da enumeração [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) `StatisticsTarget`.  
  
|Nome amigável em StatisticsTarget|Valor numérico|  
|---------------------------------------|-------------------|  
|coluna|1|  
|Índice|2|  
|Todos|3|  
  
##  <a name="CommonProperties"></a> Propriedades comuns  
 Pacotes, tarefas e os contêineres Loop Foreach, Loop For e Sequência podem usar as enumerações a seguir para definir as propriedades especificadas.  
  
 `ForceExecutionResult` propriedade — definida usando valores da `DTSForcedExecResult` enumeração.  
  
|Nome amigável em DTSForcedExecResult|Valor numérico|  
|------------------------------------------|-------------------|  
|None|-1|  
|Êxito|0|  
|Failure|1|  
|Completion|2|  
  
 Propriedade `IsolationLevel` — Definida com o uso de valores da enumeração `IsolationLevel` do .NET Framework. Para obter mais informações, consulte a Biblioteca de Classes do .NET Framework em [Biblioteca MSDN](http://go.microsoft.com/fwlink?LinkId=17313).  
  
 `LoggingMode` propriedade — definida usando valores da `DTSLoggingMode` enumeração.  
  
|Nome amigável em DTSLoggingMode|Valor numérico|  
|-------------------------------------|-------------------|  
|UseParentSetting|0|  
|Habilitado|1|  
|Desabilitado|2|  
  
 `TransactionOption` propriedade — definida usando valores da `DTSTransactionOption` enumeração.  
  
|Nome amigável em DTSTransactionOption|Valor numérico|  
|-------------------------------------------|-------------------|  
|NotSupported|0|  
|Tem suporte|1|  
|Obrigatório|2|  
  
## <a name="related-tasks"></a>Related Tasks  
 [Adicionar ou alterar uma expressão de propriedade](add-or-change-a-property-expression.md)  
  
## <a name="see-also"></a>Consulte também  
 [Usar expressões de propriedade em pacotes](use-property-expressions-in-packages.md)   
 [Serviços de integração &#40;SSIS&#41; pacotes](../integration-services-ssis-packages.md)   
 [Contêineres do Integration Services](../control-flow/integration-services-containers.md)   
 [Tarefas do Integration Services](../control-flow/integration-services-tasks.md)   
 [Restrições de precedência](../control-flow/precedence-constraints.md)  
  
  
