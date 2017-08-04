---
title: "Transferência de Editor de tarefa de objetos do SQL Server (página objetos) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects Task Editor
ms.assetid: 8cc09118-70ac-4013-8308-d87f8411ca0c
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 67557562dd3f2efbe3c40673a835dd557f617604
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-sql-server-objects-task-editor-objects-page"></a>Editor da Tarefa Transferir Objetos do SQL Server (página Objetos)
  Use a página **Objetos** da caixa de diálogo **Editor da Tarefa Transferir Objetos do SQL Server** para especificar propriedades para copiar um ou mais objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. Tabelas, exibições, procedimentos armazenados e funções definidas pelo usuário são alguns exemplos de objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você pode copiar. Para obter mais informações sobre essa tarefa, consulte [Transfer SQL Server Objects Task](../../integration-services/control-flow/transfer-sql-server-objects-task.md).  
  
> [!NOTE]  
>  O usuário que criar a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter permissões suficientes nos objetos do servidor de origem para selecioná-los para cópia, bem como permissão para acessar o banco de dados do servidor de destino no qual os objetos serão transferidos.  
  
## <a name="static-options"></a>Opções estáticas  
 **SourceConnection**  
 Selecione um Gerenciador de conexão do SMO na lista ou clique em  **\<nova conexão... >** para criar uma nova conexão para o servidor de origem.  
  
 **SourceDatabase**  
 Selecione o banco de dados no servidor de origem do qual serão copiados os objetos.  
  
 **DestinationConnection**  
 Selecione um Gerenciador de conexão do SMO na lista ou clique em  **\<nova conexão... >** para criar uma nova conexão para o servidor de destino.  
  
 **DestinationDatabase**  
 Selecione o banco de dados no servidor de destino para o qual serão copiados os objetos.  
  
 **DropObjectsFirst**  
 Selecione se os objetos selecionados serão primeiro descartados no servidor de destino, antes de serem copiados.  
  
 **IncludeExtendedProperties**  
 Selecione se as propriedades estendidas devem ser incluídas quando os objetos forem copiados da origem para o servidor de destino.  
  
 **CopyData**  
 Selecione se os dados devem ser incluídos quando os objetos forem copiados da origem para o servidor de destino.  
  
 **ExistingData**  
 Especifique como os dados serão copiados para o servidor de destino. As opções desta propriedade estão listadas na seguinte tabela:  
  
|Value|Description|  
|-----------|-----------------|  
|**Substituir**|Os dados no servidor de destino serão substituídos.|  
|**Acrescentar**|Os dados copiados do servidor de origem serão anexados aos dados existentes no servidor de destino.|  
  
> [!NOTE]  
>  A opção **ExistingData** só ficará disponível quando **CopyData** for definido como **True**.  
  
 **CopySchema**  
 Selecione se o esquema deve ser copiado durante a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  **CopySchema** só está disponível para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UseCollation**  
 Selecione se a transferência de objetos deve incluir o agrupamento especificado no servidor de origem.  
  
 **IncludeDependentObjects**  
 Selecione se a cópia dos objetos selecionados deve ser agrupada em cascata para incluir outros objetos que dependem deles para serem copiados.  
  
 **CopyAllObjects**  
 Selecione se a tarefa deve copiar todos os objetos no banco de dados de origem especificado ou apenas objetos selecionados.  Ao definir essa opção como Falso será possível selecionar os objetos a transferir e exibir as opções dinâmicas na seção **CopyAllObjects**.  
  
 **ObjectsToCopy**  
 Expanda **ObjectsToCopy** para especificar quais objetos devem ser copiados do banco de dados de origem para o banco de dados de destino.  
  
> [!NOTE]  
>  **ObjectsToCopy** só ficará disponível quando **CopyAllObjects** for definido como **False**.  
  
 As opções para copiar os seguintes tipos de objeto têm suporte apenas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 Assemblies  
  
 Funções de partição  
  
 Esquemas de partição  
  
 Esquemas  
  
 Agregações definidas pelo usuário  
  
 Tipos definidos pelo usuário  
  
 Coleções de esquemas XML  
  
 **CopyDatabaseUsers**  
 Especifique se os usuários do banco de dados devem ser incluídos na transferência.  
  
 **CopyDatabaseRoles**  
 Especifique se as funções do banco de dados devem ser incluídas na transferência.  
  
 **CopySqlServerLogins**  
 Especifique se os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser incluídos na transferência.  
  
 **CopyObjectLevelPermissions**  
 Especifique se as permissões de nível de objeto devem ser incluídas na transferência.  
  
 **CopyIndexes**  
 Especifique se os índices devem ser incluídos na transferência.  
  
 **CopyTriggers**  
 Especifique se os gatilhos devem ser incluídos na transferência.  
  
 **CopyFullTextIndexes**  
 Especifique se os índices de texto completo devem ser incluídos na transferência.  
  
 **CopyPrimaryKeys**  
 Especifique se as chaves primárias devem ser incluídas na transferência.  
  
 **CopyForeignKeys**  
 Especifique se as chaves estrangeiras devem ser incluídas na transferência.  
  
 **GenerateScriptsInUnicode**  
 Especifique se os scripts de transferência gerados estão em formato Unicode.  
  
## <a name="dynamic-options"></a>Opções dinâmicas  
  
### <a name="copyallobjects--false"></a>CopyAllObjects = False  
 **CopyAllTables**  
 Selecione se a tarefa deve copiar todas as tabelas no banco de dados de origem especificado ou apenas as tabelas selecionadas.  
  
 **TablesList**  
 Clique para abrir a caixa de diálogo **Selecionar Tabelas** .  
  
 **CopyAllViews**  
 Selecione se a tarefa deve copiar todas as exibições no banco de dados de origem especificado ou apenas as exibições selecionadas.  
  
 **ViewsList**  
 Clique para abrir a caixa de diálogo **Selecionar Exibições** .  
  
 **CopyAllStoredProcedures**  
 Selecione se a tarefa deve copiar todos os procedimentos armazenados definidos pelo usuário no banco de dados de origem especificado ou apenas os procedimentos selecionados.  
  
 **StoredProceduresList**  
 Clique para abrir a caixa de diálogo **Selecionar Procedimentos Armazenados** .  
  
 **CopyAllUserDefinedFunctions**  
 Selecione se a tarefa deve copiar todas as funções definidas pelo usuário no banco de dados de origem especificado ou apenas as funções selecionadas.  
  
 **UserDefinedFunctionsList**  
 Clique para abrir a caixa de diálogo **Selecionar Funções Definidas pelo Usuário** .  
  
 **CopyAllDefaults**  
 Selecione se a tarefa deve copiar todos os padrões no banco de dados de origem especificado ou apenas os padrões selecionados.  
  
 **DefaultsList**  
 Clique para abrir a caixa de diálogo **Selecionar Padrões** .  
  
 **CopyAllUserDefinedDataTypes**  
 Selecione se a tarefa deve copiar todos os tipos de dados definidos pelo usuário no banco de dados de origem especificado ou apenas os tipos de dados selecionados.  
  
 **UserDefinedDataTypesList**  
 Clique para abrir a caixa de diálogo **Selecionar Tipos de Dados Definidos pelo Usuário** .  
  
 **CopyAllPartitionFunctions**  
 Selecione se a tarefa deve copiar todas as funções de partição definidas pelo usuário no banco de dados de origem especificado ou apenas as funções de partição selecionadas. Com suporte apenas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **PartitionFunctionsList**  
 Clique para abrir a caixa de diálogo **Selecionar Funções de Partição** .  
  
 **CopyAllPartitionSchemes**  
 Selecione se a tarefa deve copiar todos os esquemas de partição definidos pelo usuário no banco de dados de origem especificado ou apenas os esquemas de partição selecionados. Com suporte apenas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **PartitionSchemesList**  
 Clique para abrir a caixa de diálogo **Selecionar Esquemas de Partição** .  
  
 **CopyAllSchemas**  
 Selecione se a tarefa deve copiar todos os esquemas no banco de dados de origem especificado ou apenas os esquemas selecionados. Com suporte apenas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **SchemasList**  
 Clique para abrir a caixa de diálogo **Selecionar Esquemas** .  
  
 **CopyAllSqlAssemblies**  
 Selecione se a tarefa deve copiar todos os assemblies do SQL no banco de dados de origem especificado ou apenas os assemblies do SQL selecionados. Com suporte apenas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **SqlAssembliesList**  
 Clique para abrir a caixa de diálogo **Selecionar Assemblies do SQL** .  
  
 **CopyAllUserDefinedAggregates**  
 Selecione se a tarefa deve copiar todas as agregações definidas pelo usuário no banco de dados de origem especificado ou apenas as agregações selecionadas. Com suporte apenas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UserDefinedAggregatesList**  
 Clique para abrir a caixa de diálogo **Selecionar Agregações Definidas pelo Usuário** .  
  
 **CopyAllUserDefinedTypes**  
 Selecione se a tarefa deve copiar todos os tipos definidos pelo usuário no banco de dados de origem especificado ou apenas os tipos selecionados. Com suporte apenas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UserDefinedTypes**  
 Clique para abrir a caixa de diálogo **Selecionar Tipos Definidos pelo Usuário** .  
  
 **CopyAllXmlSchemaCollections**  
 Selecione se a tarefa deve copiar todas as coleções de Esquemas XML no banco de dados de origem especificado ou apenas as coleções de esquemas XML selecionadas. Com suporte apenas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **XmlSchemaCollectionsList**  
 Clique para abrir a caixa de diálogo **Selecionar Coleções de Esquemas XML** .  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Transferência de Editor de tarefa de objetos do SQL Server &#40; Página geral &#41;](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-general-page.md)   
 [Página expressões](../../integration-services/expressions/expressions-page.md)   
 [Formatos de dados para importação ou exportação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
