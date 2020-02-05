---
title: Constantes enumeradas em expressões de propriedade | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38ba2374821505dc3541ea05e76fd8aaecdcb5fc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297638"
---
# <a name="enumerated-constants-in-property-expressions"></a>Constantes enumeradas em expressões de propriedade

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Se as expressões de propriedade incluírem valores de uma lista de membros de enumerador, a expressão deverá usar o valor numérico do membro de enumerador em vez do nome amigável do membro. Por exemplo, se uma expressão definir a propriedade **LoggingMode** , use o valor numérico 2 em vez do nome amigável Desabilitada.  
  
 Este tópico relaciona apenas os valores numéricos equivalentes a nomes amigáveis de enumeradores cujos membros são usados normalmente em expressões de propriedade. O modelo de objeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui muitos enumeradores adicionais que podem ser usados quando você programa o modelo de objeto para criar pacotes programaticamente ou codifica elementos personalizados de pacote como tarefas e componentes de fluxo de dados.  
  
 Além das propriedades personalizadas para pacotes e objetos de pacote, a janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] inclui um conjunto de propriedades disponíveis para pacotes, tarefas e os contêineres Loop Foreach, Loop For e Sequência. As propriedades comuns que são definidas por valores de enumeradores – **ForceExecutionResult**, **LoggingMode**, **IsolationLevel** e **Transaction Option** – são listadas na seção Propriedades Comuns.  
  
 As seções a seguir fornecem informações sobre constantes enumeradas:  
  
 [Pacote](#Package)  
  
 [Enumeradores de Loop Foreach](#Foreach)  
  
 [Tarefas](#Tasks)  
  
 [Tarefas do Plano de Manutenção](#MaintenancePlanTasks)  
  
 [Propriedades comuns](#CommonProperties)  
  
##  <a name="Package"></a> Pacote  
 As tabelas a seguir relacionam os nomes amigáveis e os equivalentes em valor numérico para propriedades de pacotes definidas por você usando valores de um enumerador.  
  
 Propriedade **PackageType** – definida usando valores da enumeração **DTSPackageType**.  
  
|Nome amigável em DTSPackageType|Valor numérico|  
|-------------------------------------|-------------------|  
|Padrão|0|  
|DTSWizard|1|  
|DTSDesigner|2|  
|SQLReplication|3|  
|DTSDesigner100|5|  
|SQLDBMaint|6|  
  
 Propriedade **CheckpointUsage** – definida usando valores da enumeração **DTSCheckpointUsage**.  
  
|Nome amigável em DTSCheckpointUsage|Valor numérico|  
|-----------------------------------------|-------------------|  
|Never|0|  
|IfExists|1|  
|Sempre|2|  
  
 Propriedade **PackagePriorityClass** – definida usando valores da enumeração **DTSPriorityClass**.  
  
|Nome amigável em DTSPriorityClass|Valor numérico|  
|---------------------------------------|-------------------|  
|Padrão|0|  
|AboveNormal|1|  
|Normal|2|  
|BelowNormal|3|  
|Idle|4|  
  
 Propriedade **ProtectionLevel** – definida usando valores da enumeração **DTSProtectionLevel**.  
  
|Nome amigável em DTSProtectionLevel|Valor numérico|  
|-----------------------------------------|-------------------|  
|DontSaveSensitive|0|  
|EncryptSensitiveWithUserKey|1|  
|EncryptSensitiveWithPassword|2|  
|EncryptAllWithPassword|3|  
|EncryptAllWithUserKey|4|  
|ServerStorage|5|  
  
##  <a name="PrecedenceConstraints"></a> Restrições de precedência  
 Propriedade **EvalOp** – definida usando valores da enumeração **DTSPrecedenceEvalOp**.  
  
|Nome amigável em DTSPrecedenceEvalOp|Valor numérico|  
|------------------------------------------|-------------------|  
|Expression|1|  
|Constraint|2|  
|ExpressionAndConstraint|3|  
|ExpressionOrConstraint|4|  
  
 Propriedade **Value** – definida usando valores da enumeração **DTSExecResult**.  
  
|Nome amigável|Valor numérico|  
|-------------------|-------------------|  
|Sucesso|0|  
|Falha|1|  
|Completion|2|  
|Canceled|3|  
  
##  <a name="Foreach"></a> Enumeradores de Loop Foreach  
 O Loop Foreach inclui um conjunto de enumeradores com propriedades que podem ser definidas por expressões de propriedade.  
  
### <a name="foreach-ado-enumerator"></a>Enumerador ADO Foreach  
 Propriedade **Type** – definida usando valores da enumeração **ADOEnumerationType**.  
  
|Nome amigável em ADOEnumerationType|Valor numérico|  
|-----------------------------------------|-------------------|  
|EnumerateTables|0|  
|EnumerateAllRows|1|  
|EnumerateRowsInFirstTable|2|  
  
### <a name="foreach-nodelist-enumerator"></a>Enumerador Nodelist Foreach  
 Propriedades **SourceDocumentType**, **InnerXPathStringSourceType**e **OuterXPathStringSourceType** – definidas usando os valores da enumeração **SourceType**.  
  
|Nome amigável em SourceType|Valor numérico|  
|---------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
|DirectInput|2|  
  
 Propriedade **EnumerationType** – definida usando valores da enumeração **EnumerationType**.  
  
|Nome amigável em EnumerationType|Valor numérico|  
|--------------------------------------|-------------------|  
|Navegador|0|  
|Nó|1|  
|NodeText|2|  
|ElementCollection|3|  
  
 Propriedade **InnerElementType** – definida usando valores da enumeração **InnerElementType**.  
  
|Nome amigável em InnerElementType|Valor numérico|  
|---------------------------------------|-------------------|  
|Navegador|0|  
|Nó|1|  
|NodeText|2|  
  
##  <a name="Tasks"></a> Tarefas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui várias tarefas com propriedades que podem ser definidas por expressões de propriedade.  
  
### <a name="analysis-services-execute-ddl-task"></a>Tarefa Executar DDL do Analysis Services  
 Propriedade **SourceType** – definida usando valores da enumeração **DDLSourceType**.  
  
|Nome amigável em DDLSourceType|Valor numérico|  
|------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variável|2|  
  
### <a name="bulk-insert-task"></a>Tarefa Inserção em Massa  
 Propriedade **DataFileType** – definida usando valores da enumeração **DTSBulkInsert_DataFileType**.  
  
|Nome amigável em DTSBulkInsert_DataFileType|Valor numérico|  
|--------------------------------------------------|-------------------|  
|DTSBulkInsert_DataFileType_Char|0|  
|DTSBulkInsert_DataFileType_Native|1|  
|DTSBulkInsert_DataFileType_WideChar|2|  
|DTSBulkInsert_DataFileType_WideNative|3|  
  
### <a name="execute-sql-task"></a>Tarefa Executar SQL  
 Propriedade **ResultSetType** – definida usando valores da enumeração **ResultSetType**.  
  
|Nome amigável em ResultSetType|Valor numérico|  
|------------------------------------|-------------------|  
|ResultSetType_None|1|  
|ResultSetType_SingleRow|2|  
|ResultSetType_Rowset|3|  
|ResultSetType_XML|4|  
  
 Propriedade **SqlStatementSourceType** – definida usando valores da enumeração **SqlStatementSourceType**.  
  
|Nome amigável em SqlStatementSourceType|Valor numérico|  
|---------------------------------------------|-------------------|  
|DirectInput|1|  
|FileConnection|2|  
|Variável|3|  
  
### <a name="file-system-task"></a>Tarefa Sistema de Arquivos  
 Propriedade **Operation** – definida usando valores da enumeração **DTSFileSystemOperation**.  
  
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
  
 Propriedade **Attributes** – definida usando valores da enumeração **DTSFileSystemAttributes**.  
  
|Nome amigável em DTSFileSystemAttributes|Valor numérico|  
|----------------------------------------------|-------------------|  
|Normal|0|  
|Archive|1|  
|Hidden|2|  
|ReadOnly|4|  
|Sistema|8|  
  
### <a name="ftp-task"></a>Tarefa FTP  
 Propriedade **Operation** – definida usando valores da enumeração **DTSFTPOp**.  
  
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
 Propriedade **MessageType** – definida usando valores da enumeração **MQMessageType**.  
  
|Nome amigável em MQMessageType|Valor numérico|  
|------------------------------------|-------------------|  
|DTSMQMessageType_String|0|  
|DTSMQMessageType_DataFile|1|  
|DTSMQMessageType_Variables|2|  
|DTSMQMessagType_StringMessageToVariable|3|  
  
 Propriedade **StringCompareType** – definida usando valores da enumeração **MQStringMessageCompare**.  
  
|Nome amigável em MQStringMessageCompare|Valor numérico|  
|---------------------------------------------|-------------------|  
|DTSMQStringMessageCompare_None|0|  
|DTSMQStringMessageCompare_Exact|1|  
|DTSMQStringMessageCompare_IgnoreCase|2|  
|DTSMQStringMessageCompare_Contains|3|  
  
 Propriedade **TaskType** – definida usando valores da enumeração **MQType**.  
  
|Nome amigável em MQType|Valor numérico|  
|-----------------------------|-------------------|  
|DTSMQType_Sender|0|  
|DTSMQType_Receiver|1|  
  
### <a name="send-mail-task"></a>Tarefa Enviar Email  
 Propriedade **MessageSourceType** – definida usando valores da enumeração **SendMailMessageSourceType**.  
  
|Nome amigável em SendMailMessageSourceType|Valor numérico|  
|------------------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variável|2|  
  
 Propriedade **Priority** – definida usando valores da enumeração **MailPriority**.  
  
|Nome amigável em MailPriority|Valor numérico|  
|-----------------------------------|-------------------|  
|Alta|1|  
|Normal|3|  
|Baixo|5|  
  
### <a name="transfer-database-task"></a>Tarefa Transferir Banco de Dados  
 Propriedade **Action** – definida usando valores da enumeração **TransferAction**.  
  
|Nome amigável em TransferAction|Valor numérico|  
|-------------------------------------|-------------------|  
|Cópia|0|  
|Mover|1|  
  
 Propriedade **Method** – definida usando valores da enumeração **TransferMethod**.  
  
|Nome amigável em TransferMethod|Valor numérico|  
|-------------------------------------|-------------------|  
|DatabaseOffline|0|  
|DatabaseOnline|1|  
  
### <a name="transfer-error-messages-task"></a>Tarefa Transferir Mensagens de Erro  
 Propriedade **IfObjectExists** – definida usando valores da enumeração **IfObjectExists**.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-jobs-task"></a>Tarefa Transferir Trabalhos  
 Propriedade **IfObjectExists** – definida usando valores da enumeração **IfObjectExists**.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-logins-task"></a>Tarefa Transferir Logons  
 Propriedade **IfObjectExists** – definida usando valores da enumeração **IfObjectExists**.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
 Propriedade **LoginsToTransfer** – definida usando valores da enumeração **LoginsToTransfer**.  
  
|Nome amigável em LoginsToTransfer|Valor numérico|  
|---------------------------------------|-------------------|  
|AllLogins|0|  
|SelectedLogins|1|  
|AllLoginsFromSelectedDatabases|2|  
  
### <a name="transfer-master-stored-procedures-task"></a>Tarefa Transferir Procedimentos Armazenados Mestres  
 Propriedade **IfObjectExists** – definida usando valores da enumeração **IfObjectExists**.  
  
|Nome amigável em IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-sql-server-objects-task"></a>Tarefa Transferir Objetos do SQL Server  
 Propriedade **ExistingData** – definida pelos valores da enumeração **ExistingData**.  
  
|Nome amigável em ExistingData|Valor numérico|  
|-----------------------------------|-------------------|  
|Substitua|0|  
|Acrescentar|1|  
  
### <a name="web-service-task"></a>Tarefa Serviços Web  
 Propriedade **OutputType** – definida usando valores da enumeração **DTSOutputType**.  
  
|Nome amigável em DTSOutputType|Valor numérico|  
|------------------------------------|-------------------|  
|Arquivo|0|  
|Variável|1|  
  
### <a name="wmi-data-reader-task"></a>Tarefa Leitor de Dados do WMI  
 Propriedade **OverwriteDestination** – definida usando os valores da enumeração **OverwriteDestination**.  
  
|Nome amigável em OverwriteDestination|Valor numérico|  
|-------------------------------------------|-------------------|  
|OverwriteDestination|0|  
|AppendToDestination|1|  
|KeepOriginal|2|  
  
 Propriedade**OutputType** – definida usando valores da enumeração **OutputType**.  
  
|Nome amigável em OutputType|Valor numérico|  
|---------------------------------|-------------------|  
|DataTable|0|  
|PropertyValue|1|  
|PropertyNameAndValue|2|  
  
 Propriedade **DestinationType** – definida usando valores da enumeração **DestinationType**.  
  
|Nome amigável em DestinationType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
  
 Propriedade **WqlQuerySourceType** – definida usando valores da enumeração **QuerySourceType**.  
  
|Nome amigável em QuerySourceType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variável|2|  
  
 Propriedade **ActionAtEvent** do Detector de Eventos do WMI – definida usando valores da enumeração **ActionAtEvent**.  
  
|Nome amigável em ActionAtEvent|Valor numérico|  
|------------------------------------|-------------------|  
|LogTheEventAndFireDTSEvent|0|  
|LogTheEvent|1|  
  
 Propriedade **ActionAtTimeout** – definida usando valores da enumeração **ActionAtTimeout**.  
  
|Nome amigável em ActionAtTimeout|Valor numérico|  
|--------------------------------------|-------------------|  
|LogTimeoutAndFireDTSEvent|0|  
|LogTimeout|1|  
  
 Propriedade **AfterEvent** – definida usando valores da enumeração **AfterEvent**.  
  
|Nome amigável em AfterEvent|Valor numérico|  
|---------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 Propriedade **AfterTimeout** – definida usando valores da enumeração **AfterTimeout**.  
  
|Nome amigável em AfterTimeout|Valor numérico|  
|-----------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 Propriedade **WqlQuerySourceType** – definida usando valores da enumeração **QuerySourceType**.  
  
|Nome amigável em QuerySourceType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variável|2|  
  
### <a name="xml-task"></a>XML Task  
 Propriedade **OperationType** – definida usando valores da enumeração **DTSXMLOperation**.  
  
|Nome amigável em DTSXMLOperation|Valor numérico|  
|--------------------------------------|-------------------|  
|Validar|0|  
|XSLT|1|  
|XPATH|2|  
|Mesclar|3|  
|Diff|4|  
|Patch|5|  
  
 Propriedades **SourceType**, **SecondOperandType** e **XPathSourceType** – definidas usando valores da enumeração **DTSXMLSourceType**.  
  
|Nome amigável em DTSXMLSourceType|Valor numérico|  
|---------------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
|DirectInput|2|  
  
 Propriedades **DestinationType** e **DiffGramDestinationType** – definidas usando valores da enumeração **DTSXMLSaveResultTo**.  
  
|Nome amigável em DTSXMLSaveResultTo|Valor numérico|  
|-----------------------------------------|-------------------|  
|FileConnection|0|  
|Variável|1|  
  
 Propriedade **ValidationType** – definida usando valores da enumeração **DTSXMLValidationType**.  
  
|Nome amigável em DTSXMLValidationType|Valor numérico|  
|-------------------------------------------|-------------------|  
|DTD|0|  
|XSD|1|  
  
 Propriedade **XPathOperation** – definida usando valores da enumeração **DTSXMLXPathOperation**.  
  
|Nome amigável em DTSXMLXPathOperation|Valor numérico|  
|-------------------------------------------|-------------------|  
|Avaliação|0|  
|Valores|1|  
|NodeList|2|  
  
 Propriedade **DiffOptions** – definida usando valores da enumeração **DTSXMLDiffOptions**. As opções deste enumerador não são mutuamente exclusivas. Para usar várias opções, forneça uma lista separada por vírgulas das opções a serem aplicadas.  
  
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
  
 Propriedade **DiffAlgorithm** – definida usando valores da enumeração **DTSXMLDiffAlgorithm**.  
  
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
  
 Propriedade **DatabaseSelectionType** – definida usando valores da enumeração **DatabaseSelection**.  
  
|Nome amigável em DatabaseSelection|Valor numérico|  
|----------------------------------------|-------------------|  
|Nenhum|0|  
|Todos|1|  
|Sistema|2|  
|Usuário|3|  
|Específicas|4|  
  
 Propriedade **TableSelectionType** – definida usando valores da enumeração **TableSelection**.  
  
|Nome amigável em TableSelection|Valor numérico|  
|-------------------------------------|-------------------|  
|Nenhum|0|  
|Todos|1|  
|Específicas|2|  
  
 Propriedade **ObjectTypeSelection** – definida usando valores da enumeração **ObjectType**.  
  
|Nome amigável em ObjectType|Valor numérico|  
|---------------------------------|-------------------|  
|Tabela|0|  
|Visualizar|1|  
|TableView|2|  
  
### <a name="back-up-database-task"></a>Tarefa de Backup de Banco de Dados  
 Propriedade **DestinationCreationType** – definida usando valores da enumeração **DestinationType**.  
  
|Nome amigável em DestinationType|Valor numérico|  
|--------------------------------------|-------------------|  
|Auto|0|  
|Manual|1|  
  
 Propriedade **ExistingBackupsAction** – definida usando valores da enumeração **ActionForExistingBackups**.  
  
|Nome amigável em ActionForExistingBackups|Valor numérico|  
|-----------------------------------------------|-------------------|  
|Acrescentar|0|  
|Overwrite|1|  
  
 Propriedade **BackupAction** – definida usando valores da enumeração **BackupTaskType**. Esta propriedade trabalha com a propriedade **BackupIsIncremental** para definir o tipo de backup que a tarefa executa.  
  
|Nome amigável em BackupTaskType|Valor numérico|  
|-------------------------------------|-------------------|  
|Banco de dados|0|  
|Arquivos|1|  
|Log|2|  
  
 Propriedade **BackupDevice** – definida usando valores de SMO (Objetos de Gerenciamento) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], enumeração **DeviceType**.  
  
|Nome amigável em DeviceType|Valor numérico|  
|---------------------------------|-------------------|  
|LogicalDevice|0|  
|Tape|1|  
|Arquivo|2|  
|Pipe|3|  
|VirtualDevice|4|  
  
### <a name="maintenance-cleanup-task"></a>Tarefa Limpeza de Manutenção  
 Propriedade **FileTypeSelected** – definida usando valores da enumeração **FileType**.  
  
|Nome amigável em FileType|Valor numérico|  
|-------------------------------|-------------------|  
|FileBackup|0|  
|FileReport|1|  
  
 Propriedade **OlderThanTimeUnitType** – definida usando valores da enumeração **TimeUnitType**.  
  
|Nome amigável em TimeUnitType|Valor numérico|  
|-----------------------------------|-------------------|  
|Dia|0|  
|Semana|1|  
|Month|2|  
|Ano|3|  
  
### <a name="update-statistics-task"></a>Tarefa Atualizar Estatísticas  
 Propriedade **UpdateType** – definida usando valores de SMO (Gerenciamento de Objetos) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], enumeração **StatisticsTarget**.  
  
|Nome amigável em StatisticsTarget|Valor numérico|  
|---------------------------------------|-------------------|  
|Coluna|1|  
|Índice|2|  
|Todos|3|  
  
##  <a name="CommonProperties"></a> Propriedades comuns  
 Pacotes, tarefas e os contêineres Loop Foreach, Loop For e Sequência podem usar as enumerações a seguir para definir as propriedades especificadas.  
  
 Propriedade **ForceExecutionResult** – definida usando valores da enumeração **DTSForcedExecResult**.  
  
|Nome amigável em DTSForcedExecResult|Valor numérico|  
|------------------------------------------|-------------------|  
|Nenhum|-1|  
|Sucesso|0|  
|Falha|1|  
|Completion|2|  
  
 Propriedade **IsolationLevel** – definida usando valores da enumeração **IsolationLevel** do .NET Framework. Para obter mais informações, consulte a Biblioteca de Classes do .NET Framework em [Biblioteca MSDN](https://go.microsoft.com/fwlink?LinkId=17313).  
  
 Propriedade **LoggingMode** – definida usando valores da enumeração **DTSLoggingMode**.  
  
|Nome amigável em DTSLoggingMode|Valor numérico|  
|-------------------------------------|-------------------|  
|UseParentSetting|0|  
|habilitado|1|  
|Desabilitado|2|  
  
 Propriedade **TransactionOption** – definida usando valores da enumeração **DTSTransactionOption**.  
  
|Nome amigável em DTSTransactionOption|Valor numérico|  
|-------------------------------------------|-------------------|  
|NotSupported|0|  
|Suportado|1|  
|Obrigatório|2|  
  
## <a name="related-tasks"></a>Related Tasks  
 [Adicionar ou alterar uma expressão de propriedade](../../integration-services/expressions/add-or-change-a-property-expression.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md)   
 [Pacotes do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)   
 [Contêineres do Integration Services](../../integration-services/control-flow/integration-services-containers.md)   
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Restrições de precedência](../../integration-services/control-flow/precedence-constraints.md)  
  
  
