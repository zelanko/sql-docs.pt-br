---
title: Constantes enumeradas em expressões de propriedade | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], expressions
- dynamic properties
- updating package properties
- enumerated constants [Integration Services]
- property expressions [Integration Services]
ms.assetid: a4418315-38e2-4ad3-8784-576163b25d6f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b22e25ad9053ed4da0187035cff00ff7e3ca70af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62898894"
---
# <a name="enumerated-constants-in-property-expressions"></a>Constantes enumeradas em expressões de propriedade
  Se as expressões de propriedade incluírem valores de uma lista de membros de enumerador, a expressão deverá usar o valor numérico do membro de enumerador em vez do nome amigável do membro. Por exemplo, se uma expressão definir a propriedade `LoggingMode`, use o valor numérico 2 em vez do nome amigável Desabilitada.  
  
 Este tópico relaciona apenas os valores numéricos equivalentes a nomes amigáveis de enumeradores cujos membros são usados normalmente em expressões de propriedade. O modelo de objeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui muitos enumeradores adicionais que podem ser usados quando você programa o modelo de objeto para criar pacotes programaticamente ou codifica elementos personalizados de pacote como tarefas e componentes de fluxo de dados.  
  
 Além das propriedades personalizadas para pacotes e objetos de pacote, a janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] inclui um conjunto de propriedades disponíveis para pacotes, tarefas e os contêineres Loop Foreach, Loop For e Sequência. As propriedades comuns que são definidas por valores de enumeradores-`ForceExecutionResult`, `LoggingMode`, `IsolationLevel`e `Transaction Option`-são listadas na seção Propriedades comuns.  
  
 As seções a seguir fornecem informações sobre constantes enumeradas:  
  
 [Pacote](#Package)  
  
 [Enumeradores de Loop Foreach](#Foreach)  
  
 [Tarefas](#Tasks)  
  
 [Tarefas do Plano de Manutenção](#MaintenancePlanTasks)  
  
 [Propriedades comuns](#CommonProperties)  
  
##  <a name="package"></a><a name="Package"></a> Pacote  
 As tabelas a seguir relacionam os nomes amigáveis e os equivalentes em valor numérico para propriedades de pacotes definidas por você usando valores de um enumerador.  
  
 `PackageType`Propriedade-definido usando valores da `DTSPackageType` enumeração.  
  
|Nome amigável em DTSPackageType|Valor numérico|  
|-------------------------------------|-------------------|  
|Padrão|0|  
|DTSWizard|1|  
|DTSDesigner|2|  
|SQLReplication|3|  
|DTSDesigner100|5|  
|SQLDBMaint|6|  
  
 `CheckpointUsage`Propriedade-definido usando valores da `DTSCheckpointUsage` enumeração.  
  
|Nome amigável em DTSCheckpointUsage|Valor numérico|  
|-----------------------------------------|-------------------|  
|Never|0|  
|IfExists|1|  
|Sempre|2|  
  
 `PackagePriorityClass`Propriedade-definido usando valores da `DTSPriorityClass` enumeração.  
  
|Nome amigável em DTSPriorityClass|Valor numérico|  
|---------------------------------------|-------------------|  
|Padrão|0|  
|AboveNormal|1|  
|Normal|2|  
|BelowNormal|3|  
|Idle|4|  
  
 `ProtectionLevel`Propriedade-definido usando valores da `DTSProtectionLevel` enumeração.  
  
|Nome amigável em DTSProtectionLevel|Valor numérico|  
|-----------------------------------------|-------------------|  
|DontSaveSensitive|0|  
|EncryptSensitiveWithUserKey|1|  
|EncryptSensitiveWithPassword|2|  
|EncryptAllWithPassword|3|  
|EncryptAllWithUserKey|4|  
|ServerStorage|5|  
  
##  <a name="precedence-constraints"></a><a name="PrecedenceConstraints"></a> Restrições de precedência  
 `EvalOp`Propriedade-definido usando valores da `DTSPrecedenceEvalOp` enumeração.  
  
|Nome amigável em DTSPrecedenceEvalOp|Valor numérico|  
|------------------------------------------|-------------------|  
|Expression|1|  
|Constraint|2|  
|ExpressionAndConstraint|3|  
|ExpressionOrConstraint|4|  
  
 `Value`Propriedade-definido usando valores da `DTSExecResult` enumeração.  
  
|Nome amigável|Valor numérico|  
|-------------------|-------------------|  
|Sucesso|0|  
|Falha|1|  
|Completion|2|  
|Canceled|3|  
  
##  <a name="foreach-loop-enumerators"></a><a name="Foreach"></a> Enumeradores de Loop Foreach  
 O Loop Foreach inclui um conjunto de enumeradores com propriedades que podem ser definidas por expressões de propriedade.  
  
### <a name="foreach-ado-enumerator"></a>Enumerador ADO Foreach  
 `Type`Propriedade-definido usando valores da `ADOEnumerationType` enumeração.  
  
|Nome amigável em ADOEnumerationType|Valor numérico|  
|-----------------------------------------|-------------------|  
|EnumerateTables|0|  
|EnumerateAllRows|1|  
|EnumerateRowsInFirstTable|2|  
  
### <a name="foreach-nodelist-enumerator"></a>Enumerador Nodelist Foreach  
 `SourceDocumentType`, `InnerXPathStringSourceType`e **OuterXPathStringSourceType** propriedades – definidas usando valores da `SourceType` enumeração.  
  
|Nome amigável em SourceType|Valor numérico|  
|---------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
|DirectInput|2|  
  
 `EnumerationType`Propriedade-definido usando valores da `EnumerationType` enumeração.  
  
|Nome amigável em EnumerationType|Valor numérico|  
|--------------------------------------|-------------------|  
|Navegador|0|  
|Nó|1|  
|NodeText|2|  
|ElementCollection|3|  
  
 `InnerElementType`Propriedade-definido usando valores da `InnerElementType` enumeração.  
  
|Nome amigável em InnerElementType|Valor numérico|  
|---------------------------------------|-------------------|  
|Navegador|0|  
|Nó|1|  
|NodeText|2|  
  
##  <a name="tasks"></a><a name="Tasks"></a> Tarefas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui várias tarefas com propriedades que podem ser definidas por expressões de propriedade.  
  
### <a name="analysis-services-execute-ddl-task"></a>Tarefa Executar DDL do Analysis Services  
 `SourceType`Propriedade-definido usando valores da `DDLSourceType` enumeração.  
  
|Nome amigável em DDLSourceType|Valor numérico|  
|------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variável|2|  
  
### <a name="bulk-insert-task"></a>Tarefa Inserção em Massa  
 `DataFileType`Propriedade-definido usando valores da `DTSBulkInsert_DataFileType` enumeração.  
  
|Nome amigável em DTSBulkInsert_DataFileType|Valor numérico|  
|--------------------------------------------------|-------------------|  
|DTSBulkInsert_DataFileType_Char|0|  
|DTSBulkInsert_DataFileType_Native|1|  
|DTSBulkInsert_DataFileType_WideChar|2|  
|DTSBulkInsert_DataFileType_WideNative|3|  
  
### <a name="execute-sql-task"></a>Tarefa Executar SQL  
 `ResultSetType`Propriedade-definido usando valores da `ResultSetType` enumeração.  
  
|Nome amigável em ResultSetType|Valor numérico|  
|------------------------------------|-------------------|  
|ResultSetType_None|1|  
|ResultSetType_SingleRow|2|  
|ResultSetType_Rowset|3|  
|ResultSetType_XML|4|  
  
 `SqlStatementSourceType`Propriedade-definido usando valores da `SqlStatementSourceType` enumeração.  
  
|Nome amigável em SqlStatementSourceType|Valor numérico|  
|---------------------------------------------|-------------------|  
|DirectInput|1|  
|FileConnection|2|  
|Variável|3|  
  
### <a name="file-system-task"></a>Tarefa Sistema de Arquivos  
 `Operation`Propriedade-definido usando valores da `DTSFileSystemOperation` enumeração.  
  
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
  
 `Attributes`Propriedade-definido usando valores da `DTSFileSystemAttributes` enumeração.  
  
|Nome amigável em DTSFileSystemAttributes|Valor numérico|  
|----------------------------------------------|-------------------|  
|Normal|0|  
|Archive|1|  
|Hidden|2|  
|ReadOnly|4|  
|Sistema|8|  
  
### <a name="ftp-task"></a>Tarefa FTP  
 `Operation`Propriedade-definido usando valores da `DTSFTPOp` enumeração.  
  
|Nome amigável em DTSFTPOp|Valor numérico|  
|-------------------------------|-------------------|  
|Enviar|0|  
|Receber|1|  
|DeleteLocal|2|  
|DeleteRemote|3|  
|MakeDirLocal|4|  
|MakeDirRemote|5|  
|RemoveDirLocal|6|  
|RemoveDirRemote|7|  
  
### <a name="message-queue-task"></a>Message Queue Task  
 `MessageType`Propriedade-definido usando valores da `MQMessageType` enumeração.  
  
|Nome amigável em MQMessageType|Valor numérico|  
|------------------------------------|-------------------|  
|DTSMQMessageType_String|0|  
|DTSMQMessageType_DataFile|1|  
|DTSMQMessageType_Variables|2|  
|DTSMQMessagType_StringMessageToVariable|3|  
  
 `StringCompareType`Propriedade-definido usando valores da `MQStringMessageCompare` enumeração.  
  
|Nome amigável em MQStringMessageCompare|Valor numérico|  
|---------------------------------------------|-------------------|  
|DTSMQStringMessageCompare_None|0|  
|DTSMQStringMessageCompare_Exact|1|  
|DTSMQStringMessageCompare_IgnoreCase|2|  
|DTSMQStringMessageCompare_Contains|3|  
  
 `TaskType`Propriedade-definido usando valores da `MQType` enumeração.  
  
|Nome amigável em MQType|Valor numérico|  
|-----------------------------|-------------------|  
|DTSMQType_Sender|0|  
|DTSMQType_Receiver|1|  
  
### <a name="send-mail-task"></a>Tarefa Enviar Email  
 `MessageSourceType`Propriedade-definido usando valores da `SendMailMessageSourceType` enumeração.  
  
|Nome amigável em SendMailMessageSourceType|Valor numérico|  
|------------------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variável|2|  
  
 `Priority`Propriedade-definido usando valores da `MailPriority` enumeração.  
  
|Nome amigável em MailPriority|Valor numérico|  
|-----------------------------------|-------------------|  
|Alta|1|  
|Normal|3|  
|Baixo|5|  
  
### <a name="transfer-database-task"></a>Tarefa Transferir Banco de Dados  
 `Action`Propriedade-definido usando valores da `TransferAction` enumeração.  
  
|Nome amigável em TransferAction|Valor numérico|  
|-------------------------------------|-------------------|  
|Cópia|0|  
|Mover|1|  
  
 `Method`Propriedade-definido usando valores da `TransferMethod` enumeração.  
  
|Nome amigável em TransferMethod|Valor numérico|  
|-------------------------------------|-------------------|  
|DatabaseOffline|0|  
|DatabaseOnline|1|  
  
### <a name="transfer-error-messages-task"></a>Tarefa Transferir Mensagens de Erro  
 `IfObjectExists`Propriedade-definido usando valores da `IfObjectExists` enumeração.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-jobs-task"></a>Tarefa Transferir Trabalhos  
 `IfObjectExists`Propriedade-definido usando valores da `IfObjectExists` enumeração.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-logins-task"></a>Tarefa Transferir Logons  
 `IfObjectExists`Propriedade-definido usando valores da `IfObjectExists` enumeração.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
 `LoginsToTransfer`Propriedade-definido usando valores da `LoginsToTransfer` enumeração.  
  
|Nome amigável em LoginsToTransfer|Valor numérico|  
|---------------------------------------|-------------------|  
|AllLogins|0|  
|SelectedLogins|1|  
|AllLoginsFromSelectedDatabases|2|  
  
### <a name="transfer-master-stored-procedures-task"></a>Tarefa Transferir Procedimentos Armazenados Mestres  
 `IfObjectExists`Propriedade-definido usando valores da `IfObjectExists` enumeração.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-sql-server-objects-task"></a>Tarefa Transferir Objetos do SQL Server  
 `ExistingData`Propriedade-definido usando valores da `ExistingData` enumeração.  
  
|Nome amigável em ExistingData|Valor numérico|  
|-----------------------------------|-------------------|  
|Substitua|0|  
|Acrescentar|1|  
  
### <a name="web-service-task"></a>Tarefa Serviços Web  
 `OutputType`Propriedade-definido usando valores da `DTSOutputType` enumeração.  
  
|Nome amigável em DTSOutputType|Valor numérico|  
|------------------------------------|-------------------|  
|Arquivo|0|  
|Variável|1|  
  
### <a name="wmi-data-reader-task"></a>Tarefa Leitor de Dados do WMI  
 `OverwriteDestination`Propriedade-definido usando valores da `OverwriteDestination` enumeração.  
  
|Nome amigável em OverwriteDestination|Valor numérico|  
|-------------------------------------------|-------------------|  
|OverwriteDestination|0|  
|AppendToDestination|1|  
|KeepOriginal|2|  
  
 `OutputType`Propriedade-definido usando valores da `OutputType` enumeração.  
  
|Nome amigável em OutputType|Valor numérico|  
|---------------------------------|-------------------|  
|DataTable|0|  
|PropertyValue|1|  
|PropertyNameAndValue|2|  
  
 `DestinationType`Propriedade-definido usando valores da `DestinationType` enumeração.  
  
|Nome amigável em DestinationType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
  
 `WqlQuerySourceType`Propriedade-definido usando valores da `QuerySourceType` enumeração.  
  
|Nome amigável em QuerySourceType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variável|2|  
  
 `ActionAtEvent` Propriedade do Inspetor de eventos do WMI – definida usando valores da `ActionAtEvent` enumeração.  
  
|Nome amigável em ActionAtEvent|Valor numérico|  
|------------------------------------|-------------------|  
|LogTheEventAndFireDTSEvent|0|  
|LogTheEvent|1|  
  
 `ActionAtTimeout`Propriedade-definido usando valores da `ActionAtTimeout` enumeração.  
  
|Nome amigável em ActionAtTimeout|Valor numérico|  
|--------------------------------------|-------------------|  
|LogTimeoutAndFireDTSEvent|0|  
|LogTimeout|1|  
  
 `AfterEvent`Propriedade-definido usando valores da `AfterEvent` enumeração.  
  
|Nome amigável em AfterEvent|Valor numérico|  
|---------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 `AfterTimeout`Propriedade-definido usando valores da `AfterTimeout` enumeração.  
  
|Nome amigável em AfterTimeout|Valor numérico|  
|-----------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 `WqlQuerySourceType`Propriedade-definido usando valores da `QuerySourceType` enumeração.  
  
|Nome amigável em QuerySourceType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variável|2|  
  
### <a name="xml-task"></a>XML Task  
 `OperationType`Propriedade-definido usando valores da `DTSXMLOperation` enumeração.  
  
|Nome amigável em DTSXMLOperation|Valor numérico|  
|--------------------------------------|-------------------|  
|Validar|0|  
|XSLT|1|  
|XPATH|2|  
|Mesclar|3|  
|Diff|4|  
|Patch|5|  
  
 `SourceType`Propriedades `SecondOperandType`, e `XPathSourceType` -define usando valores da `DTSXMLSourceType` enumeração.  
  
|Nome amigável em DTSXMLSourceType|Valor numérico|  
|---------------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
|DirectInput|2|  
  
 `DestinationType`e propriedades de **DiffGramDestinationType** – definidas usando valores da `DTSXMLSaveResultTo` enumeração.  
  
|Nome amigável em DTSXMLSaveResultTo|Valor numérico|  
|-----------------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
  
 `ValidationType`Propriedade-definido usando valores da `DTSXMLValidationType` enumeração.  
  
|Nome amigável em DTSXMLValidationType|Valor numérico|  
|-------------------------------------------|-------------------|  
|DTD|0|  
|XSD|1|  
  
 `XPathOperation`Propriedade-definido usando valores da `DTSXMLXPathOperation` enumeração.  
  
|Nome amigável em DTSXMLXPathOperation|Valor numérico|  
|-------------------------------------------|-------------------|  
|Avaliação|0|  
|Valores|1|  
|NodeList|2|  
  
 `DiffOptions`Propriedade-definido usando valores da `DTSXMLDiffOptions` enumeração. As opções deste enumerador não são mutuamente exclusivas. Para usar várias opções, forneça uma lista separada por vírgulas das opções a serem aplicadas.  
  
|Nome amigável em DTSXMLDiffOptions|Valor numérico|  
|----------------------------------------|-------------------|  
|Nenhum|0|  
|IgnoreChildOrder|1|  
|IgnoreComments|2|  
|IgnorePI|4|  
|IgnoreWhitespace|8|  
|IgnoreNamespaces|16|  
|IgnorePrefixes|32|  
|IgnoreXmlDecl|64|  
|IgnoreDtd|128|  
  
 `DiffAlgorithm`Propriedade-definido usando valores da `DTSXMLDiffAlgorithm` enumeração.  
  
|Nome amigável em DTSXMLDiffAlgorithm|Valor numérico|  
|------------------------------------------|-------------------|  
|Auto|0|  
|Rápido|1|  
|Preciso|2|  
  
##  <a name="maintenance-plan-tasks"></a><a name="MaintenancePlanTasks"></a> Tarefas do Plano de Manutenção  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui um conjunto de tarefas que executam tarefas do SQL Server para uso em planos de manutenção e pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte ao trabalho programático com essas tarefas e a documentação de referência de programação não inclui documentação da API dessas tarefas e seus enumeradores.  
  
### <a name="all-maintenance-tasks"></a>Todas as Tarefas de Manutenção  
 Todas as tarefas de manutenção usam as enumerações a seguir para definir as propriedades especificadas.  
  
 `DatabaseSelectionType`Propriedade-definido usando valores da `DatabaseSelection` enumeração.  
  
|Nome amigável em DatabaseSelection|Valor numérico|  
|----------------------------------------|-------------------|  
|Nenhum|0|  
|Todos|1|  
|Sistema|2|  
|Usuário|3|  
|Específicas|4|  
  
 `TableSelectionType`Propriedade-definido usando valores da `TableSelection` enumeração.  
  
|Nome amigável em TableSelection|Valor numérico|  
|-------------------------------------|-------------------|  
|Nenhum|0|  
|Todos|1|  
|Específicas|2|  
  
 `ObjectTypeSelection`Propriedade-definido usando valores da `ObjectType` enumeração.  
  
|Nome amigável em ObjectType|Valor numérico|  
|---------------------------------|-------------------|  
|Tabela|0|  
|Visualizar|1|  
|TableView|2|  
  
### <a name="back-up-database-task"></a>Tarefa de Backup de Banco de Dados  
 `DestinationCreationType`Propriedade-definido usando valores da `DestinationType` enumeração.  
  
|Nome amigável em DestinationType|Valor numérico|  
|--------------------------------------|-------------------|  
|Auto|0|  
|Manual|1|  
  
 `ExistingBackupsAction`Propriedade-definido usando valores da `ActionForExistingBackups` enumeração.  
  
|Nome amigável em ActionForExistingBackups|Valor numérico|  
|-----------------------------------------------|-------------------|  
|Acrescentar|0|  
|Overwrite|1|  
  
 `BackupAction`Propriedade-definido usando valores da `BackupTaskType` enumeração. Esta propriedade trabalha com a propriedade `BackupIsIncremental` para definir o tipo de backup que a tarefa executa.  
  
|Nome amigável em BackupTaskType|Valor numérico|  
|-------------------------------------|-------------------|  
|Banco de dados|0|  
|Arquivos|1|  
|Log|2|  
  
 `BackupDevice`Propriedade-definido usando valores da enumeração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Smo (Management Objects `DeviceType` ).  
  
|Nome amigável em DeviceType|Valor numérico|  
|---------------------------------|-------------------|  
|LogicalDevice|0|  
|Tape|1|  
|Arquivo|2|  
|Pipe|3|  
|VirtualDevice|4|  
  
### <a name="maintenance-cleanup-task"></a>Tarefa Limpeza de Manutenção  
 `FileTypeSelected`Propriedade-definido usando valores da `FileType` enumeração.  
  
|Nome amigável em FileType|Valor numérico|  
|-------------------------------|-------------------|  
|FileBackup|0|  
|FileReport|1|  
  
 `OlderThanTimeUnitType`Propriedade-definido usando valores da `TimeUnitType` enumeração.  
  
|Nome amigável em TimeUnitType|Valor numérico|  
|-----------------------------------|-------------------|  
|Dia|0|  
|Semana|1|  
|Month|2|  
|Ano|3|  
  
### <a name="update-statistics-task"></a>Tarefa Atualizar Estatísticas  
 `UpdateType`Propriedade-definido usando valores da enumeração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Smo (Management Objects `StatisticsTarget` ).  
  
|Nome amigável em StatisticsTarget|Valor numérico|  
|---------------------------------------|-------------------|  
|Coluna|1|  
|Índice|2|  
|Todos|3|  
  
##  <a name="common-properties"></a><a name="CommonProperties"></a> Propriedades comuns  
 Pacotes, tarefas e os contêineres Loop Foreach, Loop For e Sequência podem usar as enumerações a seguir para definir as propriedades especificadas.  
  
 `ForceExecutionResult`Propriedade-definido usando valores da `DTSForcedExecResult` enumeração.  
  
|Nome amigável em DTSForcedExecResult|Valor numérico|  
|------------------------------------------|-------------------|  
|Nenhum|-1|  
|Sucesso|0|  
|Falha|1|  
|Completion|2|  
  
 `IsolationLevel`Propriedade-definida pela enumeração de `IsolationLevel` .NET Framework. Para obter mais informações, consulte a Biblioteca de Classes do .NET Framework em [Biblioteca MSDN](https://go.microsoft.com/fwlink?LinkId=17313).  
  
 `LoggingMode`Propriedade-definido usando valores da `DTSLoggingMode` enumeração.  
  
|Nome amigável em DTSLoggingMode|Valor numérico|  
|-------------------------------------|-------------------|  
|UseParentSetting|0|  
|habilitado|1|  
|Desabilitado|2|  
  
 `TransactionOption`Propriedade-definido usando valores da `DTSTransactionOption` enumeração.  
  
|Nome amigável em DTSTransactionOption|Valor numérico|  
|-------------------------------------------|-------------------|  
|NotSupported|0|  
|Suportado|1|  
|Obrigatório|2|  
  
## <a name="related-tasks"></a>Related Tasks  
 [Adicionar ou alterar uma expressão de propriedade](add-or-change-a-property-expression.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Usar expressões de propriedade em pacotes](use-property-expressions-in-packages.md)   
 [Pacotes do Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md)   
 [Contêineres do Integration Services](../control-flow/integration-services-containers.md)   
 [Tarefas do Integration Services](../control-flow/integration-services-tasks.md)   
 [Restrições de precedência](../control-flow/precedence-constraints.md)  
  
  
