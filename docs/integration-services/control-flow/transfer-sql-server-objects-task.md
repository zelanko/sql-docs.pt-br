---
title: Transferir tarefa de objetos do SQL Server | Microsoft Docs
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
- sql13.dts.designer.transfersqlserverobjectstask.f1
- sql13.dts.designer.transfersqlserverobjects.general.f1
- sql13.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: fd7916034970aba3a64d66ee2b59a1661d8a9515
ms.contentlocale: pt-br
ms.lasthandoff: 08/11/2017

---
# <a name="transfer-sql-server-objects-task"></a>Tarefa Transferir Objetos do SQL Server
  A tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transfere um ou mais tipos de objetos para um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, a tarefa pode copiar tabelas e procedimentos armazenados. Dependendo da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado como fonte, tipos diferentes de objetos estarão disponíveis para cópia. Por exemplo, só um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui esquemas e agregações definidos pelo usuário.  
  
## <a name="objects-to-transfer"></a>Objetos a serem transferidos  
 Funções de servidor, funções e usuários do banco de dados especificado poderão ser copiados, bem como as permissões para os objetos transferidos. Copiando os usuários, as funções e as permissões associados juntamente com os objetos, os objetos transferidos ficarão imediatamente operáveis no servidor de destino.  
  
 A tabela a seguir lista os tipos de objetos que podem ser copiados.  
  
|Objeto|  
|------------|  
|Tabelas|  
|Exibições|  
|Procedimentos armazenados|  
|Funções definidas pelo usuário|  
|Padrões|  
|Tipos de dados definidos pelo usuário|  
|Funções de partição|  
|Esquemas de partição|  
|Esquemas|  
|Assemblies|  
|Agregações definidas pelo usuário|  
|Tipos definidos pelo usuário|  
|Coleção de esquema XML|  
  
 Os UDTs (Tipos Definidos pelo Usuário) criados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm dependências em assemblies CLR (Common Language Runtime). Se você usar a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para transferir UDTs, terá de configurar a tarefa para transferir objetos dependentes. Para transferir objetos dependentes, defina a propriedade **IncludeDependentObjects** como **True**.  
  
### <a name="table-options"></a>Opções de tabela  
 Ao copiar tabelas, você poderá indicar os tipos de itens relacionados a tabelas a serem incluídos no processo de cópia. Os seguintes tipos de itens poderão ser copiados com a tabela relacionada:  
  
-   Índices  
  
-   Gatilhos  
  
-   Índices de texto completo  
  
-   Chaves primárias  
  
-   Chaves estrangeiras  
  
 Você também poderá indicar que o script gerado pela tarefa tenha o formato Unicode.  
  
## <a name="destination-options"></a>Opções de destino  
 Você pode configurar a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para incluir nomes de esquema, dados, propriedades estendidas de objetos transferidos e objetos dependentes na transferência. Se forem copiados dados, ela poderá substituir ou anexar dados existentes.  
  
 Algumas opções só se aplicam ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, somente o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a esquemas.  
  
## <a name="security-options"></a>Opções de segurança  
 A tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode incluir usuários em nível de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e funções da fonte, logons [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e permissões para objetos transferidos. Por exemplo, a transferência pode incluir as permissões nas tabelas transferidas.  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>Transferir objetos entre instâncias do SQL Server  
 A tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a uma origem e a um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 A tarefa ativa um evento de informações que informa o objeto transferido e um evento de aviso quando um objeto é substituído. Um evento de informações também é ativado para ações como o truncamento de tabelas de banco de dados.  
  
 A tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não informa progresso incremental da transferência do objeto; informa somente conclusão 0% e 100 % .  
  
## <a name="execution-value"></a>Valor de execução  
 O valor de execução armazenado na propriedade da tarefa **ExecutionValue** retorna o número de objetos transferidos. Ao atribuir uma variável definida pelo usuário à propriedade **ExecValueVariable** da tarefa Transferir Objetos do SQL Server, as informações sobre a transferência do objeto podem ser disponibilizadas para outros objetos do pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas de log  
 A tarefa Transferir Objetos do SQL inclui as seguintes entradas de log personalizadas:  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects   Essa entrada de log informa que a transferência foi iniciada. A entrada do log contém a hora de início.  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects    Essa entrada de log informa que a transferência foi concluída. A entrada do log contém a hora de término.  
  
 Além disso, uma entrada de log para um evento **OnInformation** informa o número de objetos dos tipos de objeto selecionados para transferência, o número de objetos transferidos e ações como truncamento de tabelas quando são transferidos dados com tabelas. Uma entrada de log para o evento **OnWarning** é gravada para cada objeto de destino que é substituído  
  
## <a name="security-and-permissions"></a>Segurança e permissões  
 O usuário deve ter permissão para procurar objetos no servidor de origem e deve ter permissão para cancelar e criar objetos no servidor de destino; além disso, o usuário deve ter acesso ao banco de dados especificado e aos objetos do banco de dados.  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>Configuração da tarefa Transferir Objetos do SQL Server  
 A tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser configurada para transferir todos os objetos, todos os objetos de um tipo ou somente objetos especificados de um tipo. Por exemplo, você pode escolher copiar somente tabelas selecionadas no banco de dados AdventureWorks.  
  
 Se a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transferir tabelas, você poderá especificar os tipos de objetos relacionados à tabela a serem copiados com as tabelas. Por exemplo, você poderá especificar que as chaves primárias sejam copiadas com as tabelas.  
  
 Para aprimorar a funcionalidade dos objetos transferidos, você pode configurar a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para incluir nomes de esquema, dados, propriedades estendidas de objetos transferidos e objetos dependentes na transferência. Ao copiar os dados, você poderá especificar se os dados existentes deverão ser substituídos ou anexados.  
  
 No tempo de execução, a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz a conexão com os servidores de origem e destino usando dois gerenciadores de conexões SMO. Os gerenciadores de conexões SMO são configurados separadamente da tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e referenciadas na tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os gerenciadores de conexões SMO especificam o servidor e o modo de autenticação a serem usados ao acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>Configuração programática da tarefa Transferir Objetos do SQL Server  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
## <a name="transfer-sql-server-objects-task-editor-general-page"></a>Editor da Tarefa Transferir Objetos do SQL Server (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Transferir Objetos do SQL Server** para nomear e descrever a tarefa Transferir Objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  É necessário que o usuário que criar a tarefa Transferir Objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenha as permissões adequadas nos objetos de servidor de origem para selecioná-las para cópia, e permissão para acessar o banco de dados do servidor de destino para o qual os objetos serão transferidos.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Digite um nome exclusivo para a tarefa Transferir Objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Description**  
 Digite uma descrição da tarefa Transferir Objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="transfer-sql-server-objects-task-editor-objects-page"></a>Editor da Tarefa Transferir Objetos do SQL Server (página Objetos)
  Use a página **Objetos** da caixa de diálogo **Editor da Tarefa Transferir Objetos do SQL Server** para especificar propriedades para copiar um ou mais objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra. Tabelas, exibições, procedimentos armazenados e funções definidas pelo usuário são alguns exemplos de objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você pode copiar.  
  
> [!NOTE]  
>  O usuário que criar a tarefa Transferir Objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter permissões suficientes nos objetos do servidor de origem para selecioná-los para cópia, bem como permissão para acessar o banco de dados do servidor de destino no qual os objetos serão transferidos.  
  
### <a name="static-options"></a>Opções estáticas  
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
  
### <a name="dynamic-options"></a>Opções dinâmicas  
  
#### <a name="copyallobjects--false"></a>CopyAllObjects = False  
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

