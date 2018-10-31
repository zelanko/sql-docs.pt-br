---
title: SqlPackage.exe | Microsoft Docs
ms.prod: sql
ms.technology: ssdt
ms.date: 2018-06-27
ms.reviewer: alayu; sstein
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: b7bf75b16a9c7962ce1d04f51182d21107daa181
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051218"
---
# <a name="sqlpackageexe"></a>SqlPackage.exe

O **SqlPackage.exe** é um utilitário de linha de comando que automatiza as seguintes tarefas de desenvolvimento de banco de dados:  
  
- [Extract](#help-for-the-extract-action): cria um arquivo (.dacpac) de instantâneo de um banco de dados do SQL Server dinâmico ou do Banco de Dados SQL do Azure.  
  
- [Publish](#publish-parameters-properties-and-sqlcmd-variables): atualiza um esquema de banco de dados incrementalmente para que corresponda ao esquema de um arquivo .dacpac de origem. Se o banco de dados não existir no servidor, a operação de publicação irá criá-lo. Caso contrário, o banco de dados existente é atualizado.  
  
- [Export](#export-parameters-and-properties): exporta um banco de dados dinâmico – incluindo o esquema e os dados de usuário do banco de dados – do SQL Server ou do Banco de Dados SQL do Azure para um pacote BACPAC (arquivo .bacpac).  
  
- [Import](#import-parameters-and-properties): importa os dados de esquema e tabela de um pacote BACPAC para um novo banco de dados do usuário em uma instância do SQL Server ou do Banco de Dados SQL do Azure.  
  
- [DeployReport](#deployreport-parameters-and-properties): cria um relatório XML das alterações que teriam sido feitas por uma ação de publicação.  
  
- [DriftReport](#driftreport-parameters): cria um relatório XML das alterações que teriam sido feitas a um banco de dados registrado desde a última vez que ele foi registrado.  
  
- [Script](#script-parameters-and-properties): cria um script de atualização incremental Transact-SQL que atualiza o esquema de um destino para que corresponda ao esquema de uma origem.  
  
A linha de comando do **SqlPackage.exe** permite que você especifique essas ações junto com parâmetros e propriedades específicos da ação.  

**[Baixe a versão mais recente](sqlpackage-download.md)**. Para obter detalhes sobre a versão mais recente, consulte o [notas de versão](sqlpackage-release-notes.md).
  
## <a name="command-line-syntax"></a>Sintaxe da linha de comando

O **SqlPackage.exe** inicia as ações especificadas usando os parâmetros, as propriedades e as variáveis SQLCMD especificados na linha de comando.  
  
```
SqlPackage {parameters}{properties}{SQLCMD Variables}  
```
  
### <a name="help-for-the-extract-action"></a>Ajuda para a ação de extração

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Extract|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/ DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/ MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação; {NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action: publicar /?. |
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão. |
|**/ SourceConnectionString:**|**/SCS**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/SDN**|{string}|Define o nome do banco de dados de origem. |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/ SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/ SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo SSL a ser usado para criptografar a conexão de banco de dados de origem e ignorar a verificação cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/ TargetFile:**|**/tf**|{string}| Especifica um arquivo de destino (ou seja, um arquivo. dacpac) a ser usado como o destino da ação, em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de destino será válido. Esse parâmetro será válido para ações que só oferecem suporte a destinos de banco de dados.| 
|**/TenantId:**|**/tid**|{string}|Representa o nome de ID ou o domínio de locatário do AD do Azure. Essa opção é necessária para dar suporte a convidado ou importados de usuários do AD do Azure, bem como contas da Microsoft como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário do AD do Azure padrão será usada, supondo que o usuário autenticado é um usuário nativo para esse anúncio. No entanto, nesse caso, qualquer convidado ou os usuários importados e/ou contas da Microsoft hospedadas nesse Azure AD não têm suporte e a operação falhará. <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação Universal deve ser usada. Quando definido como True, o protocolo de autenticação interativa é ativado que dão suporte a MFA. Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo exigir que o usuário insira seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication é definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/ scs). Quando /UniversalAuthentication é definido como False, a autenticação do Azure AD deve ser especificada no SourceConnectionString (/ scs). <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|

### <a name="properties-specific-to-the-extract-action"></a>Propriedades específicas para a ação de extração

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|CommandTimeout = (INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.|
|**/p:**|DacApplicationDescription=(STRING)|Define a descrição do aplicativo a ser armazenada nos metadados do DACPAC.|
|**/p:**|DacApplicationName=(STRING)|Definiu o nome do aplicativo a ser armazenado nos metadados do DACPAC. O valor padrão é o nome do banco de dados.|
|**/p:**|DacMajorVersion = (INT32 '1')|Define a versão principal a ser armazenada nos metadados do DACPAC.|
|**/p:**|DacMinorVersion = (INT32 '0')|Define a versão secundária a ser armazenada nos metadados do DACPAC.|
|**/p:**|ExtractAllTableData=(BOOLEAN)|Indica se os dados de todas as tabelas de usuário são extraídos. Se for 'true', os dados de todas as tabelas de usuário são extraídos e não é possível especificar tabelas de usuário individual para extração de dados. Se for 'false', especifique uma ou mais tabelas de usuário para extrair dados.|
|**/p:**|ExtractApplicationScopedObjectsOnly = (BOOLIANO ' True')|Se for verdadeiro, apenas extrairá objetos com escopo para o aplicativo da origem especificada. Se for falso, extrairá todos os objetos com escopo para o aplicativo da origem especificada.|
|**/p:**|ExtractReferencedServerScopedElements = (BOOLIANO ' True')|Se true, extrairá logon, auditoria de servidor e objetos de credencial referenciados pelos objetos do banco de dados de origem.|
|**/p:**|ExtractUsageProperties=(BOOLEAN)|Especifica se propriedades de uso, como contagem de linhas da tabela e tamanho do índice, serão extraídas do banco de dados.|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|Especifica se as propriedades estendidas devem ser ignoradas.|
|**/p:**|IgnorePermissions = (BOOLIANO ' True')|Especifica se as permissões devem ser ignoradas.|
|**/p:**|IgnoreUserLoginMappings=(BOOLEAN)|Especifica se os relacionamentos entre usuários e logons devem ser ignorados.|
|**/p:**|Armazenamento = ({arquivo&#124;memória} 'File')|Especifica o tipo de armazenamento de backup para o modelo de esquema usado durante a extração.|
|**/p:**|TableData=(STRING)|Indica a tabela da qual os dados serão extraídos. Especifique o nome da tabela, com ou sem os colchetes ao redor das partes do nome no seguinte formato: identificador_tabela.|
|**/p:**|VerifyExtraction=(BOOLEAN)|Especifica se o dacpac extraído deve ser verificado.|

## <a name="publish-parameters-properties-and-sqlcmd-variables"></a>Parâmetro, propriedades e variáveis SQLCMD de publicação

Uma operação de publicação SqlPackage.exe atualiza o esquema de um banco de dados de destino incrementalmente para que corresponda à estrutura de um banco de dados de origem. A publicação de um pacote de implantação que contenha dados de usuário para todos ou para um subconjunto das tabelas atualizará os dados da tabela além do esquema. A implantação de dados substitui o esquema e os dados em tabelas existentes do banco de dados de destino. A implantação de dados não alterará o esquema existente ou os dados no banco de dados de destino para tabelas que não são incluídas no pacote de implantação.  

### <a name="help-for-publish-action"></a>Ajuda para a ação de publicação

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Publicar|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/ AzureKeyVaultAuthMethod:**|**/akv**|{Interativo&#124;ClientIdSecret}|Especifica o método de autenticação que é usado para acessar o Azure Key Vault |
|**/ClientId:**|**/CID**|{string}|Especifica a ID do Cliente a ser usada na autenticação no Azure Key Vault, quando necessário |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/ DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/ MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Profile:**|**/pr**|{string}|Especifica o caminho de um arquivo para um perfil de publicação do DAC. O perfil define uma coleção de propriedades e variáveis para serem usadas ao gerar saídas.|
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação;{NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action: publicar /?.|
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/Secret:**|**/secr**|{string}|Especifica o Segredo do Cliente a ser usado na autenticação no Azure Key Vault, quando necessário |
|**/ SourceConnectionString:**|**/SCS**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/SDN**|{string}|Define o nome do banco de dados de origem. |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/ Arquivo de origem:**|**/sf**|{string}|Especifica um arquivo de origem a ser usado como origem da ação, em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de origem deverá ser válido. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/ SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/ SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo SSL a ser usado para criptografar a conexão de banco de dados de origem e ignorar a verificação cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/ TargetConnectionString:**|**/TCS**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/ TargetEncryptConnection:**|**/Tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/ TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/ TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/ TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. Para o Azure AD, é recomendável que esse valor seja maior que ou igual a 30 segundos.|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se SSL será usado para criptografar a conexão de banco de dados de destino e ignorar a cadeia de certificados para validar a confiança. |
|**/ TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de ID ou o domínio de locatário do AD do Azure. Essa opção é necessária para dar suporte a convidado ou importados de usuários do AD do Azure, bem como contas da Microsoft como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário do AD do Azure padrão será usada, supondo que o usuário autenticado é um usuário nativo para esse anúncio. No entanto, nesse caso, qualquer convidado ou os usuários importados e/ou contas da Microsoft hospedadas nesse Azure AD não têm suporte e a operação falhará. <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação Universal deve ser usada. Quando definido como True, o protocolo de autenticação interativa é ativado que dão suporte a MFA. Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo exigir que o usuário insira seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication é definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/ scs). Quando /UniversalAuthentication é definido como False, a autenticação do Azure AD deve ser especificada no SourceConnectionString (/ scs). <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/Variables:**|**/v**|{PropertyName}={Value}|Especifica um par nome-valor para uma variável específica de ação;{NomeDaVariável}={Valor}. O arquivo DACPAC contém a lista de variáveis SQLCMD válidas. Ocorrerá um erro se não for fornecido um valor para cada variável. |

### <a name="properties-specific-to-the-publish-action"></a>Propriedades específicas para a ação de publicação

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|Especifica argumentos adicionais de colaborador de implantação para os colaboradores de implantação. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula.|
|**/p:**|AdditionalDeploymentContributors=(STRING)|Especifica colaboradores adicionais de implantação que devem ser executados quando o DACPAC é implantado. Ele deve ser em formato de lista delimitada por ponto e vírgula com os IDs ou nomes totalmente qualificados do colaborador de compilação.|
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|Essa propriedade é usada pela implantação de SqlClr para descartar os assemblies com bloqueio como parte do plano de implantação. Por padrão, os assemblies de bloqueio/referência bloquearão uma atualização de assembly se o assembly de referência precisar ser descartado.|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|Especifica se a ação deve continuar apesar de plataformas do SQL Server potencialmente incompatíveis.|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|Não bloqueie a movimentação de dados em uma tabela que tenha Segurança em Nível de Linha se essa propriedade estiver definida como true. O padrão é false.|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|Faz backups do banco de dados antes de implantar qualquer alteração.|
|**/p:**|BlockOnPossibleDataLoss = (BOOLIANO ' True')|Especifica que o episódio de publicação deverá ser terminado se houver uma possibilidade de perda de dados resultante da operação de publicação.|
|**/p:**|BlockWhenDriftDetected = (BOOLIANO ' True')|Especifica se deve bloquear a atualização de um banco de dados cujo esquema não mais corresponda seu registro ou não esteja registrado.|
|**/p:**|CommandTimeout = (INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.|
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|Especifica se a declaração de variáveis SETVAR devem ser comentadas no script de publicação gerado. Você pode optar por fazer isso se planejar especificar os valores na linha de comando ao publicar usando uma ferramenta como SQLCMD.EXE.|
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|Essa configuração dita como a ordenação do banco de dados é tratada durante a implantação; por padrão, a ordenação do banco de dados de destino será atualizada se não corresponder à ordenação especificada pela origem. Quando essa opção estiver configurada, a ordenação do banco de dados de destino (ou do servidor) deverá ser usada.|
|**/p:**|CreateNewDatabase=(BOOLEAN)|Especifica se o banco de dados de destino deve ser atualizado ou removido e recriado quando um banco de dados é publicado.|
|**/p:**|DatabaseEdition = ({Basic&#124;Standard&#124;Premium&#124;padrão} 'Default')|Define a edição de um banco de dados do SQL Azure.|
|**/p:**|DatabaseMaximumSize=(INT32)|Define o tamanho máximo, em GB, de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseServiceObjective=(STRING)|Define o nível de desempenho de um Banco de Dados SQL do Azure, como "P0" ou "S1".|
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|Se for verdadeiro, o banco de dados será definido como o Modo de Usuário Único antes da implantação.|
|**/p:**|DisableAndReenableDdlTriggers = (BOOLIANO ' True')|Especifica se os gatilhos da DDL (linguagem de definição de dados) são desabilitados no início do processo de publicação e reabilitados no final da ação de publicação.|
|**/p:**|DoNotAlterChangeDataCaptureObjects = (BOOLIANO ' True')|Se for verdadeiro, os objetos do Change Data Capture não serão alterados.|
|**/p:**|DoNotAlterReplicatedObjects = (BOOLIANO ' True')|Especifica se os objetos que forem replicados são identificados durante a verificação.|
|**/p:**|DoNotDropObjectType=(STRING)|Um tipo de objeto que não deve ser descartado quando DropObjectsNotInSource está definido como true. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|DoNotDropObjectTypes=(STRING)|Uma lista separada por ponto e vírgula de tipos de objeto que não devem ser removidos quando DropObjectsNotInSource é true. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|DropConstraintsNotInSource = (BOOLIANO ' True')|Especifica se as restrições que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropDmlTriggersNotInSource = (BOOLIANO ' True')|Especifica se os gatilhos DML que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publica em um banco de dados.|
|**/p:**|DropExtendedPropertiesNotInSource = (BOOLIANO ' True')|Especifica se as propriedades estendidas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropIndexesNotInSource = (BOOLIANO ' True')|Especifica se os índices que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|Especifica se os objetos que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar em um banco de dados. Esse valor prevalece sobre DropExtendedProperties.|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|Especifica se as permissões que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|Especifica se os membros de função que não estão definidos no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropStatisticsNotInSource = (BOOLIANO ' True')|Especifica se as estatísticas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|ExcludeObjectType=(STRING)|Um tipo de objeto que deve ser ignorado durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|ExcludeObjectTypes=(STRING)|Uma lista, delimitada por ponto e vírgula, de tipos de objetos que devem ser ignorados durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|Automaticamente fornece um valor padrão ao atualizar uma tabela que contém dados com uma coluna que não permite valores nulos.|
|**/p:**|IgnoreAnsiNulls = (BOOLIANO ' True')|Especifica se diferenças na configuração ANSI NULLS deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|Especifica se diferenças no Autorizador deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|Especifica se diferenças nas ordenações de coluna deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|Especifica se as diferenças na ordem das colunas da tabela devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|
|**/p:**|IgnoreComments=(BOOLEAN)|Especifica se diferenças nos comentários deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreCryptographicProviderFilePath = (BOOLIANO ' True')|Especifica se as diferenças no caminho do arquivo para o provedor de criptografia deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um servidor ou banco de dados.|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|Especifica se diferenças no esquema padrão deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DML (linguagem de manipulação de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DML deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|Especifica se diferenças nas propriedades estendidas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFileAndLogFilePath = (BOOLIANO ' True')|Especifica se diferenças nos caminhos para arquivos e arquivos de log deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFilegroupPlacement = (BOOLIANO ' True')|Especifica se diferenças no posicionamento de objetos em FILEGROUPs deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFileSize = (BOOLIANO ' True')|Especifica se diferenças nos tamanhos de arquivos deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.|
|**/p:**|IgnoreFillFactor = (BOOLIANO ' True')|Especifica se diferenças no fator de preenchimento de armazenamento de índice deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.|
|**/p:**|IgnoreFullTextCatalogFilePath = (BOOLIANO ' True')|Especifica se diferenças no caminho do arquivo do catálogo de texto completo deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|Especifica se diferenças na semente de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar atualizações em um banco de dados.|
|**/p:**|IgnoreIncrement=(BOOLEAN)|Especifica se diferenças no incremento de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|Especifica se diferenças nas opções de índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreIndexPadding = (BOOLIANO ' True')|Especifica se diferenças nas opções de preenchimento do índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreKeywordCasing = (BOOLIANO ' True')|Especifica se diferenças no uso de maiúsculas e minúsculas em palavras-chave deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|Especifica se diferenças no uso de dicas de bloqueio em índices deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreLoginSids = (BOOLIANO ' True')|Especifica se diferenças no número SID (identificação de segurança) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|Especifica se as configurações que não sejam para replicação deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme = (BOOLIANO ' True')|Especifica se o posicionamento de um objeto em um esquema de partição deverá ser ignorado ou atualizado quando você publicar em um banco de dados.|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|Especifica se diferenças em esquemas de partição e funções deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnorePermissions=(BOOLEAN)|Especifica se diferenças nas permissões deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreQuotedIdentifiers = (BOOLIANO ' True')|Especifica se diferenças na configuração de identificadores entre aspas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|Especifica se as diferenças nas associações de logons à função devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|
|**/p:**|IgnoreRouteLifetime = (BOOLIANO ' True')|Especifica se diferenças na quantidade de tempo que o SQL Server retém a rota na tabela de roteamento deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreSemicolonBetweenStatements = (BOOLIANO ' True')|Especifica se diferenças nos pontos e vírgulas entre instruções T-SQL serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|Especifica se diferenças nas opções de tabela serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|Especifica se diferenças nos objetos de configurações do usuário serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreWhitespace = (BOOLIANO ' True')|Especifica se diferenças de espaço em branco serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para restrições de verificação serão ignoradas ou atualizadas quando você publicar.|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para chaves estrangeiras serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|Inclua todos os elementos compostos como parte de uma única operação de publicação.|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|Especifica se instruções transacionais deverão ser usadas quando possível quando você publicar em um banco de dados.|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|Especifica se a publicação sempre deverá cancelar e recriar um assembly se houver uma diferença em vez de emitir uma instrução ALTER ASSEMBLY.|
|**/p:**|PopulateFilesOnFileGroups = (BOOLIANO ' True')|Especifica se um novo arquivo também será criado quando um novo FileGroup for criado no banco de dados de destino.|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|Especifica se o esquema está registrado com o servidor de banco de dados.|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|Especifica se os colaboradores de DeploymentPlanExecutor devem ser executados quando outras operações são executadas.|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|Especifica se diferenças na ordenação do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|Especifica se diferenças na compatibilidade do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|ScriptDatabaseOptions = (BOOLIANO ' True')|Especifica se as propriedades do banco de dados de destino devem ser definidas ou atualizadas como parte da ação de publicação.|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|Especifica se as instruções são geradas no script de publicação para verificar se o nome do banco de dados e o nome do servidor correspondem aos nomes especificados no projeto de banco de dados.|
|**/p:**|ScriptFileSize=(BOOLEAN)|Controla se o tamanho é especificado ao adicionar um arquivo a um grupo de arquivos.|
|**/p:**|ScriptNewConstraintValidation = (BOOLIANO ' True')|No final da publicação, todas as restrições serão verificadas em conjunto, evitando erros de dados causados por uma verificação ou uma restrição de chave estrangeira no meio da publicação. Se definido como False, as restrições serão publicadas sem verificar os dados correspondentes.|
|**/p:**|ScriptRefreshModule = (BOOLIANO ' True')|Inclua instruções de atualização no fim do script de publicação.|
|**/p:**|Armazenamento = ({arquivo&#124;memória})|Especifica como os elementos são armazenados ao criar o modelo de banco de dados. Por razões de desempenho, o padrão é InMemory. Para bancos de dados grandes, é necessário realizar armazenamento de backup de arquivos.|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|Especifica se os erros encontrados durante a publicação verificação deve ser tratada como avisos. A verificação é executada em relação ao plano de implantação gerado antes de o plano ser executado em relação ao banco de dados de destino. A verificação do plano detecta problemas, como a perda de objetos apenas de destino (por exemplo, índices), que devem ser cancelados para fazer uma alteração. A verificação também detectará situações em que existem dependências (como tabelas ou exibições) devido a uma referência a um projeto composto, mas não existem no banco de dados de destino. Você pode optar por fazer isso para obter uma lista completa de todos os problemas, em vez de ter a ação de publicação parar no primeiro erro.|**/p:**|UnmodifiableObjectWarnings = (BOOLIANO ' True')|Especifica se devem ser gerados avisos quando diferenças forem localizadas em objetos que não podem ser modificados, por exemplo, se o tamanho ou os caminhos de arquivo forem diferentes para um arquivo.|
|**/p:**|VerifyCollationCompatibility = (BOOLIANO ' True')|Especifica se a compatibilidade de ordenação é verificada.|
|**/p:**|VerifyDeployment = (BOOLIANO ' True')|Especifica se devem ser executadas verificações antes da publicação, o que interromperá a ação de publicação se houver problemas que possam bloquear uma publicação bem-sucedida. Por exemplo, sua ação de publicação poderá ser interrompida se você tiver chaves estrangeiras no banco de dados de destino que não existem no projeto de banco de dados, o que causará erros ao publicar.|
|

### <a name="sqlcmd-variables"></a>Variáveis SQLCMD

A tabela a seguir descreve o formato da opção que pode ser usada para substituir o valor de uma variável de comando SQL (**sqlcmd**) usada durante uma ação de publicação. Os valores da variável especificados na linha de comando substituem outros valores atribuídos à variável (por exemplo, em um perfil de publicação).  
  
|Parâmetro|Padrão|Descrição|  
|-------------|-----------|---------------|  
|**/ Variáveis: {PropertyName} = {Value}**||Especifica um par nome-valor para uma variável específica de ação; {NomeDaVariável}={Valor}. O arquivo DACPAC contém a lista de variáveis SQLCMD válidas. Ocorrerá um erro se não for fornecido um valor para cada variável.|  
  
## <a name="export-parameters-and-properties"></a>Parâmetros e propriedades de exportação

Uma ação de exportação SqlPackage.exe exporta um banco de dados dinâmico do SQL Server ou banco de dados SQL a um pacote (arquivo. bacpac). Por padrão, os dados de todas as tabelas serão incluídos no arquivo .bacpac. Como opção, você pode especificar apenas um subconjunto das tabelas para o qual exportará dados. A validação para a ação Exportar garante a compatibilidade do Banco de Dados SQL do Azure para o banco de dados de destino completo, mesmo que esteja especificado um subconjunto das tabelas para a exportação.  
  
### <a name="help-for-export-action"></a>Ajuda para a ação de exportação

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Exportar|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/ DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/ MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação;{NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action: publicar /?.|
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/ SourceConnectionString:**|**/SCS**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/SDN**|{string}|Define o nome do banco de dados de origem. |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/ SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/ SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo SSL a ser usado para criptografar a conexão de banco de dados de origem e ignorar a verificação cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/ TargetFile:**|**/tf**|{string}| Especifica um arquivo de destino (ou seja, um arquivo. dacpac) a ser usado como o destino da ação, em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de destino será válido. Esse parâmetro será válido para ações que só oferecem suporte a destinos de banco de dados.|
|**/TenantId:**|**/tid**|{string}|Representa o nome de ID ou o domínio de locatário do AD do Azure. Essa opção é necessária para dar suporte a convidado ou importados de usuários do AD do Azure, bem como contas da Microsoft como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário do AD do Azure padrão será usada, supondo que o usuário autenticado é um usuário nativo para esse anúncio. No entanto, nesse caso, qualquer convidado ou os usuários importados e/ou contas da Microsoft hospedadas nesse Azure AD não têm suporte e a operação falhará. <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação Universal deve ser usada. Quando definido como True, o protocolo de autenticação interativa é ativado que dão suporte a MFA. Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo exigir que o usuário insira seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication é definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/ scs). Quando /UniversalAuthentication é definido como False, a autenticação do Azure AD deve ser especificada no SourceConnectionString (/ scs). <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|

### <a name="properties-specific-to-the-export-action"></a>Propriedades específicas para a ação de exportação

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|CommandTimeout = (INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.|
|**/p:**|Armazenamento = ({arquivo&#124;memória} 'File')|Especifica o tipo de armazenamento de backup para o modelo de esquema usado durante a extração.|
|**/p:**|TableData=(STRING)|Indica a tabela da qual os dados serão extraídos. Especifique o nome da tabela, com ou sem os colchetes ao redor das partes do nome no seguinte formato: identificador_tabela.|
|**/p:**|TargetEngineVersion = ({padrão&#124;versão mais recente&#124;V11&#124;V12} 'Mais recente')|Especifica qual é a versão esperada do mecanismo de destino. Isso afeta se deve permitir que objetos com suporte pelos servidores de banco de dados SQL com funcionalidades V12, como tabelas com otimização de memória, no bacpac gerado.|
|**/p:**|VerifyFullTextDocumentTypesSupported=(BOOLEAN)|Especifica se os tipos de documento de texto completo compatíveis para Banco de Dados SQL do Microsoft Azure v12 devem ser verificados.|
  
## <a name="import-parameters-and-properties"></a>Parâmetros e propriedades de importação

Uma ação de importação SqlPackage.exe importa o esquema e tabela de dados de um pacote BACPAC - arquivo. bacpac – para um banco de dados novo ou vazio no SQL Server ou banco de dados SQL. No momento da operação de importação para um banco de dados existente, o banco de dados de destino não pode conter nenhum objeto de esquema definido pelo usuário.  
  
### <a name="help-for-command-actions"></a>Ajuda para ações de comando

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Importar|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/ DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/ MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação;{NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action: publicar /?.|
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/ Arquivo de origem:**|**/sf**|{string}|Especifica um arquivo de origem a ser usado como a origem da ação. Se esse parâmetro for usado, nenhum outro parâmetro de origem deverá ser válido. |
|**/ TargetConnectionString:**|**/TCS**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/ TargetEncryptConnection:**|**/Tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/ TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/ TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/ TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. Para o Azure AD, é recomendável que esse valor seja maior que ou igual a 30 segundos.|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se SSL será usado para criptografar a conexão de banco de dados de destino e ignorar a cadeia de certificados para validar a confiança. |
|**/ TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de ID ou o domínio de locatário do AD do Azure. Essa opção é necessária para dar suporte a convidado ou importados de usuários do AD do Azure, bem como contas da Microsoft como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário do AD do Azure padrão será usada, supondo que o usuário autenticado é um usuário nativo para esse anúncio. No entanto, nesse caso, qualquer convidado ou os usuários importados e/ou contas da Microsoft hospedadas nesse Azure AD não têm suporte e a operação falhará. <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação Universal deve ser usada. Quando definido como True, o protocolo de autenticação interativa é ativado que dão suporte a MFA. Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo exigir que o usuário insira seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication é definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/ scs). Quando /UniversalAuthentication é definido como False, a autenticação do Azure AD deve ser especificada no SourceConnectionString (/ scs). <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|

Propriedades específicas para a ação de importação:
|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|CommandTimeout = (INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.|
|**/p:**|DatabaseEdition = ({Basic&#124;Standard&#124;Premium&#124;padrão} 'Default')|Define a edição de um banco de dados do SQL Azure.|
|**/p:**|DatabaseMaximumSize=(INT32)|Define o tamanho máximo, em GB, de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseServiceObjective=(STRING)|Define o nível de desempenho de um Banco de Dados SQL do Azure, como "P0" ou "S1".|
|**/p:**|ImportContributorArguments=(STRING)|Especifica argumentos adicionais de colaborador de implantação para os colaboradores de implantação. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula.|
|**/p:**|ImportContributors=(STRING)|Especifica os colaboradores de implantação que devem ser executados quando o bacpac é importado. Ele deve ser em formato de lista delimitada por ponto e vírgula com os IDs ou nomes totalmente qualificados do colaborador de compilação.|
|**/p:**|Armazenamento = ({arquivo&#124;memória})|Especifica como os elementos são armazenados ao criar o modelo de banco de dados. Por razões de desempenho, o padrão é InMemory. Para bancos de dados grandes, é necessário realizar armazenamento de backup de arquivos.|
  
## <a name="deployreport-parameters-and-properties"></a>Parâmetros e propriedades de DeployReport

Uma ação de relatório do **SqlPackage.exe** cria um relatório XML das alterações que teriam sido feitas por uma ação de publicação.  
  
### <a name="help-for-deployreport-action"></a>Ajuda para a ação de DeployReport

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|DeployReport|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/ DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/ MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/OutputPath:**|**/op**|{string}|Especifica o caminho de arquivo onde os arquivos de saída são gerados. |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Profile:**|**/pr**|{string}|Especifica o caminho de um arquivo para um perfil de publicação do DAC. O perfil define uma coleção de propriedades e variáveis para serem usadas ao gerar saídas. |
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação; {NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action: publicar /?. |
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão. |
|**/ SourceConnectionString:**|**/SCS**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/SDN**|{string}|Define o nome do banco de dados de origem. |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/ Arquivo de origem:**|**/sf**|{string}|Especifica um arquivo de origem a ser usado como origem da ação, em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de origem deverá ser válido. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/ SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/ SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo SSL a ser usado para criptografar a conexão de banco de dados de origem e ignorar a verificação cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/ TargetConnectionString:**|**/TCS**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/ TargetEncryptConnection:**|**/Tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/ TargetFile:**|**/tf**|{string}|Especifica um arquivo de destino (ou seja, um arquivo. dacpac) a ser usado como o destino da ação, em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de destino será válido. Esse parâmetro será válido para ações que só oferecem suporte a destinos de banco de dados.|
|**/ TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/ TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/ TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. Para o Azure AD, é recomendável que esse valor seja maior que ou igual a 30 segundos.|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se SSL será usado para criptografar a conexão de banco de dados de destino e ignorar a cadeia de certificados para validar a confiança. |
|**/ TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de ID ou o domínio de locatário do AD do Azure. Essa opção é necessária para dar suporte a convidado ou importados de usuários do AD do Azure, bem como contas da Microsoft como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário do AD do Azure padrão será usada, supondo que o usuário autenticado é um usuário nativo para esse anúncio. No entanto, nesse caso, qualquer convidado ou os usuários importados e/ou contas da Microsoft hospedadas nesse Azure AD não têm suporte e a operação falhará. <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação Universal deve ser usada. Quando definido como True, o protocolo de autenticação interativa é ativado que dão suporte a MFA. Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo exigir que o usuário insira seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication é definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/ scs). Quando /UniversalAuthentication é definido como False, a autenticação do Azure AD deve ser especificada no SourceConnectionString (/ scs). <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/Variables:**|**/v**|{PropertyName}={Value}|Especifica um par nome-valor para uma variável específica de ação; {NomeDaVariável}={Valor}. O arquivo DACPAC contém a lista de variáveis SQLCMD válidas. Ocorrerá um erro se não for fornecido um valor para cada variável. |

## <a name="properties-specific-to-the-deployreport-action"></a>Propriedades específicas para a ação de DeployReport

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|Especifica argumentos adicionais de colaborador de implantação para os colaboradores de implantação. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula.|
|**/p:**|AdditionalDeploymentContributors=(STRING)|Especifica colaboradores adicionais de implantação que devem ser executados quando o DACPAC é implantado. Ele deve ser em formato de lista delimitada por ponto e vírgula com os IDs ou nomes totalmente qualificados do colaborador de compilação.|
|**/p:**|AllowDropBlocking Assemblies=(BOOLEAN)|Essa propriedade é usada pela implantação de SqlClr para descartar os assemblies com bloqueio como parte do plano de implantação. Por padrão, os assemblies de bloqueio/referência bloquearão uma atualização de assembly se o assembly de referência precisar ser descartado.|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|Especifica se a ação deve continuar apesar de plataformas do SQL Server potencialmente incompatíveis.|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|Não bloqueie a movimentação de dados em uma tabela que tenha Segurança em Nível de Linha se essa propriedade estiver definida como true. O padrão é false.|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|Faz backups do banco de dados antes de implantar qualquer alteração.|
|**/p:**|BlockOnPossibleDataLoss = (BOOLIANO ' True')|Especifica que o episódio de publicação deverá ser terminado se houver uma possibilidade de perda de dados resultante da operação de publicação.|
|**/p:**|BlockWhenDriftDetected = (BOOLIANO ' True')|Especifica se deve bloquear a atualização de um banco de dados cujo esquema não mais corresponda seu registro ou não esteja registrado. |
|**/p:**|CommandTimeout = (INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server. |
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|Especifica se a declaração de variáveis SETVAR devem ser comentadas no script de publicação gerado. Você pode optar por fazer isso se planejar especificar os valores na linha de comando ao publicar usando uma ferramenta como SQLCMD.EXE. |
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|Essa configuração dita como a ordenação do banco de dados é tratada durante a implantação; por padrão, a ordenação do banco de dados de destino será atualizada se não corresponder à ordenação especificada pela origem. Quando essa opção estiver configurada, a ordenação do banco de dados de destino (ou do servidor) deverá ser usada. |
|**/p:**|CreateNewDatabase=(BOOLEAN)|Especifica se o banco de dados de destino deve ser atualizado ou removido e recriado quando um banco de dados é publicado. |
|**/p:**|DatabaseEdition = ({Basic&#124;Standard&#124;Premium&#124;padrão} 'Default')|Define a edição de um banco de dados do SQL Azure. |
|**/p:**|DatabaseMaximumSize=(INT32)|Define o tamanho máximo, em GB, de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseServiceObjective=(STRING)|Define o nível de desempenho de um Banco de Dados SQL do Azure, assim como "P0" ou "S1". |
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|Se for verdadeiro, o banco de dados será definido como o Modo de Usuário Único antes da implantação. |
|**/p:**|DisableAndReenableDdlTriggers = (BOOLIANO ' True')| Especifica se os gatilhos da DDL (linguagem de definição de dados) são desabilitados no início do processo de publicação e reabilitados no final da ação de publicação.|
|**/p:**|DoNotAlterChangeDataCaptureObjects = (BOOLIANO ' True')|Se for verdadeiro, os objetos do Change Data Capture não serão alterados.|
|**/p:**|DoNotAlterReplicatedObjects = (BOOLIANO ' True')|Especifica se os objetos que forem replicados são identificados durante a verificação.|
|**/p:**|DoNotDropObjectType=(STRING)|Um tipo de objeto que não deve ser descartado quando DropObjectsNotInSource está definido como true. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers. |
|**/p:**|DoNotDropObjectTypes=(STRING)|Uma lista separada por ponto e vírgula de tipos de objeto que não devem ser removidos quando DropObjectsNotInSource é true. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|DropConstraintsNotInSource = (BOOLIANO ' True')|Especifica se as restrições que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropDmlTriggersNotInSource = (BOOLIANO ' True')|Especifica se os gatilhos DML que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publica em um banco de dados.|
|**/p:**|DropExtendedPropertiesNotInSource = (BOOLIANO ' True')|Especifica se as propriedades estendidas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropIndexesNotInSource = (BOOLIANO ' True')|Especifica se os índices que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|Especifica se os objetos que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar em um banco de dados. Esse valor prevalece sobre DropExtendedProperties.|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|Especifica se as permissões que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|Especifica se os membros de função que não estão definidos no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropStatisticsNotInSource = (BOOLIANO ' True')|Especifica se as estatísticas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|ExcludeObjectType=(STRING)|Um tipo de objeto que deve ser ignorado durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|ExcludeObjectTypes=(STRING)|Uma lista, delimitada por ponto e vírgula, de tipos de objetos que devem ser ignorados durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|Automaticamente fornece um valor padrão ao atualizar uma tabela que contém dados com uma coluna que não permite valores nulos.|
|**/p:**|IgnoreAnsiNulls = (BOOLIANO ' True')|Especifica se diferenças na configuração ANSI NULLS deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|Especifica se diferenças no Autorizador deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|Especifica se diferenças nas ordenações de coluna deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|Especifica se as diferenças na ordem das colunas da tabela devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|
|**/p:**|IgnoreComments=(BOOLEAN)|Especifica se diferenças nos comentários deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreCryptographicProviderFilePath = (BOOLIANO ' True')|Especifica se as diferenças no caminho do arquivo para o provedor de criptografia deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um servidor ou banco de dados.|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|Especifica se diferenças no esquema padrão deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DML (linguagem de manipulação de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DML deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|Especifica se diferenças nas propriedades estendidas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreFileAndLogFilePath = (BOOLIANO ' True')|Especifica se diferenças nos caminhos para arquivos e arquivos de log deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreFilegroupPlacement = (BOOLIANO ' True')|Especifica se diferenças no posicionamento de objetos em FILEGROUPs deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreFileSize = (BOOLIANO ' True')|Especifica se diferenças nos tamanhos de arquivos deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados. |
|**/p:**|IgnoreFillFactor = (BOOLIANO ' True')|Especifica se diferenças no fator de preenchimento de armazenamento de índice deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados|
|**/p:**|IgnoreFullTextCatalogFilePath = (BOOLIANO ' True')|Especifica se diferenças no caminho do arquivo do catálogo de texto completo deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.| 
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|Especifica se diferenças na semente de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar atualizações em um banco de dados. |
|**/p:**|IgnoreIncrement=(BOOLEAN)|Especifica se diferenças no incremento de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|Especifica se diferenças nas opções de índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreIndexPadding = (BOOLIANO ' True')|Especifica se diferenças nas opções de preenchimento do índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreKeywordCasing = (BOOLIANO ' True')|Especifica se diferenças no uso de maiúsculas e minúsculas em palavras-chave deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|Especifica se diferenças no uso de dicas de bloqueio em índices deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreLoginSids = (BOOLIANO ' True')| Especifica se diferenças no número SID (identificação de segurança) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|Especifica se as configurações que não sejam para replicação deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreObjectPlacementOnPartitionScheme = (BOOLIANO ' True')|Especifica se o posicionamento de um objeto em um esquema de partição deverá ser ignorado ou atualizado quando você publicar em um banco de dados.|
 |**/p:**|IgnorePartitionSchemes=(BOOLEAN)|Especifica se diferenças em esquemas de partição e funções deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnorePermissions=(BOOLEAN)|Especifica se diferenças nas permissões deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreQuotedIdentifiers = (BOOLIANO ' True')|Especifica se diferenças na configuração de identificadores entre aspas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|Especifica se as diferenças nas associações de logons à função devem ser ignoradas ou atualizadas quando você publica em um banco de dados. |
|**/p:**|IgnoreRouteLifetime = (BOOLIANO ' True')|Especifica se diferenças na quantidade de tempo que o SQL Server retém a rota na tabela de roteamento deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados|
|**/p:**|IgnoreSemicolonBetweenStatements = (BOOLIANO ' True')|Especifica se diferenças nos pontos e vírgulas entre instruções T-SQL serão ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreTableOptions=(BOOLEAN)|Especifica se diferenças nas opções de tabela serão ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|Especifica se diferenças nos objetos de configurações do usuário serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreWhitespace = (BOOLIANO ' True')|Especifica se diferenças de espaço em branco serão ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para restrições de verificação serão ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para chaves estrangeiras serão ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|Inclua todos os elementos compostos como parte de uma única operação de publicação.|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|Especifica se instruções transacionais deverão ser usadas quando possível quando você publicar em um banco de dados.|
 |**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|Especifica se a publicação sempre deverá cancelar e recriar um assembly se houver uma diferença em vez de emitir uma instrução ALTER ASSEMBLY. |
|**/p:**|PopulateFilesOnFileGroups = (BOOLIANO ' True')|Especifica se um novo arquivo também será criado quando um novo FileGroup for criado no banco de dados de destino. |
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|Especifica se o esquema está registrado com o servidor de banco de dados. 
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|Especifica se os colaboradores de DeploymentPlanExecutor devem ser executados quando outras operações são executadas.|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|Especifica se diferenças na ordenação do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|Especifica se diferenças na compatibilidade do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|ScriptDatabaseOptions = (BOOLIANO ' True')|Especifica se as propriedades do banco de dados de destino devem ser definidas ou atualizadas como parte da ação de publicação. |
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|Especifica se as instruções são geradas no script de publicação para verificar se o nome do banco de dados e o nome do servidor correspondem aos nomes especificados no projeto de banco de dados.|
|**/p:**|ScriptFileSize=(BOOLEAN)|Controla se o tamanho é especificado ao adicionar um arquivo a um grupo de arquivos. |
|**/p:**|ScriptNewConstraintValidation = (BOOLIANO ' True')|No final da publicação, todas as restrições serão verificadas em conjunto, evitando erros de dados causados por uma verificação ou uma restrição de chave estrangeira no meio da publicação. Se definido como False, as restrições serão publicadas sem verificar os dados correspondentes.|
|**/p:**|ScriptRefreshModule = (BOOLIANO ' True')|Inclua instruções de atualização no fim do script de publicação.|
|**/p:**|Armazenamento = ({arquivo&#124;memória})|Especifica como os elementos são armazenados ao criar o modelo de banco de dados. Por razões de desempenho, o padrão é InMemory. Para bancos de dados grandes, é necessário realizar armazenamento de backup de arquivos.|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|Especifica se os erros encontrados durante a publicação verificação deve ser tratada como avisos. A verificação é executada em relação ao plano de implantação gerado antes de o plano ser executado em relação ao banco de dados de destino. A verificação do plano detecta problemas, como a perda de objetos apenas de destino (por exemplo, índices), que devem ser cancelados para fazer uma alteração. A verificação também detectará situações em que existem dependências (como tabelas ou exibições) devido a uma referência a um projeto composto, mas não existem no banco de dados de destino. Você pode optar por fazer isso para obter uma lista completa de todos os problemas, em vez de ter a ação de publicação parar no primeiro erro. |
|**/p:**|UnmodifiableObjectWarnings = (BOOLIANO ' True')|Especifica se devem ser gerados avisos quando diferenças forem localizadas em objetos que não podem ser modificados, por exemplo, se o tamanho ou os caminhos de arquivo forem diferentes para um arquivo.| 
|**/p:**|VerifyCollationCompatibility = (BOOLIANO ' True')|Especifica se a compatibilidade de ordenação é verificada.| 
|**/p:**|VerifyDeployment = (BOOLIANO ' True')|Especifica se devem ser executadas verificações antes da publicação, o que interromperá a ação de publicação se houver problemas que possam bloquear uma publicação bem-sucedida. Por exemplo, sua ação de publicação poderá ser interrompida se você tiver chaves estrangeiras no banco de dados de destino que não existem no projeto de banco de dados, o que causará erros ao publicar. |
  
## <a name="driftreport-parameters"></a>Parâmetros DriftReport

Uma ação de relatório do **SqlPackage.exe** cria um relatório XML das alterações que teriam sido feitas a um banco de dados registrado desde a última vez que foi registrado.  
  
### <a name="help-for-driftreport-action"></a>Ajuda para a ação de DriftReport

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|DriftReport|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/ DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/ MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/OutputPath:**|**/op**|{string}|Especifica o caminho de arquivo onde os arquivos de saída são gerados. |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/ TargetConnectionString:**|**/TCS**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/ TargetEncryptConnection:**|**/Tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/ TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/ TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/ TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. Para o Azure AD, é recomendável que esse valor seja maior que ou igual a 30 segundos.|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se SSL será usado para criptografar a conexão de banco de dados de destino e ignorar a cadeia de certificados para validar a confiança. |
|**/ TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de ID ou o domínio de locatário do AD do Azure. Essa opção é necessária para dar suporte a convidado ou importados de usuários do AD do Azure, bem como contas da Microsoft como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário do AD do Azure padrão será usada, supondo que o usuário autenticado é um usuário nativo para esse anúncio. No entanto, nesse caso, qualquer convidado ou os usuários importados e/ou contas da Microsoft hospedadas nesse Azure AD não têm suporte e a operação falhará. <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação Universal deve ser usada. Quando definido como True, o protocolo de autenticação interativa é ativado que dão suporte a MFA. Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo exigir que o usuário insira seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication é definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/ scs). Quando /UniversalAuthentication é definido como False, a autenticação do Azure AD deve ser especificada no SourceConnectionString (/ scs). <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|

## <a name="script-parameters-and-properties"></a>Parâmetros e propriedades de script

Uma ação de script do **SqlPackage.exe** cria um script de atualização incremental Transact-SQL que atualiza o esquema de um banco de dados de destino para que corresponda ao esquema de um banco de dados de origem.  
  
### <a name="help-for-the-script-action"></a>Ajuda para a ação de Script

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Script|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/ DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/ MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/OutputPath:**|**/op**|{string}|Especifica o caminho de arquivo onde os arquivos de saída são gerados. |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Profile:**|**/pr**|{string}|Especifica o caminho de um arquivo para um perfil de publicação do DAC. O perfil define uma coleção de propriedades e variáveis para serem usadas ao gerar saídas.|
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação;{NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action: publicar /?.|
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/ SourceConnectionString:**|**/SCS**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/SDN**|{string}|Define o nome do banco de dados de origem. |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/ Arquivo de origem:**|**/sf**|{string}|Especifica um arquivo de origem a ser usado como a origem da ação. Se esse parâmetro for usado, nenhum outro parâmetro de origem deverá ser válido. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/ SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/ SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo SSL a ser usado para criptografar a conexão de banco de dados de origem e ignorar a verificação cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/ TargetConnectionString:**|**/TCS**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente, em lugar de todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/ TargetEncryptConnection:**|**/Tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/ TargetFile:**|**/tf**|{string}| Especifica um arquivo de destino (ou seja, um arquivo. dacpac) a ser usado como o destino da ação, em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de destino será válido. Esse parâmetro será válido para ações que só oferecem suporte a destinos de banco de dados.|
|**/ TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/ TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/ TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. Para o Azure AD, é recomendável que esse valor seja maior que ou igual a 30 segundos.|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se SSL será usado para criptografar a conexão de banco de dados de destino e ignorar a cadeia de certificados para validar a confiança. |
|**/ TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de ID ou o domínio de locatário do AD do Azure. Essa opção é necessária para dar suporte a convidado ou importados de usuários do AD do Azure, bem como contas da Microsoft como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário do AD do Azure padrão será usada, supondo que o usuário autenticado é um usuário nativo para esse anúncio. No entanto, nesse caso, qualquer convidado ou os usuários importados e/ou contas da Microsoft hospedadas nesse Azure AD não têm suporte e a operação falhará. <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação Universal deve ser usada. Quando definido como True, o protocolo de autenticação interativa é ativado que dão suporte a MFA. Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo exigir que o usuário insira seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication é definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/ scs). Quando /UniversalAuthentication é definido como False, a autenticação do Azure AD deve ser especificada no SourceConnectionString (/ scs). <br/> Para obter mais informações sobre a autenticação Universal do Active Directory, consulte [autenticação Universal com o banco de dados SQL e SQL Data Warehouse (suporte SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/Variables:**|**/v**|{PropertyName}={Value}|Especifica um par nome-valor para uma variável específica de ação;{NomeDaVariável}={Valor}. O arquivo DACPAC contém a lista de variáveis SQLCMD válidas. Ocorrerá um erro se não for fornecido um valor para cada variável. |

### <a name="properties-specific-to-the-script-action"></a>Propriedades específicas para a ação de Script

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|Especifica argumentos adicionais de colaborador de implantação para os colaboradores de implantação. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula.
|**/p:**|AdditionalDeploymentContributors=(STRING)|Especifica colaboradores adicionais de implantação que devem ser executados quando o DACPAC é implantado. Ele deve ser em formato de lista delimitada por ponto e vírgula com os IDs ou nomes totalmente qualificados do colaborador de compilação.
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|Essa propriedade é usada pela implantação de SqlClr para descartar os assemblies com bloqueio como parte do plano de implantação. Por padrão, os assemblies de bloqueio/referência bloquearão uma atualização de assembly se o assembly de referência precisar ser descartado.
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|Especifica se a ação deve continuar apesar de plataformas do SQL Server potencialmente incompatíveis.
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|Não bloqueie a movimentação de dados em uma tabela que tenha Segurança em Nível de Linha se essa propriedade estiver definida como true. O padrão é false.
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|Faz backups do banco de dados antes de implantar qualquer alteração.
|**/p:**|BlockOnPossibleDataLoss = (BOOLIANO ' True')|Especifica que o episódio de publicação deverá ser terminado se houver uma possibilidade de perda de dados resultante da operação de publicação.
|**/p:**|BlockWhenDriftDetected = (BOOLIANO ' True')|Especifica se deve bloquear a atualização de um banco de dados cujo esquema não mais corresponda seu registro ou não esteja registrado.
|**/p:**|CommandTimeout = (INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|Especifica se a declaração de variáveis SETVAR devem ser comentadas no script de publicação gerado. Você pode optar por fazer isso se planejar especificar os valores na linha de comando ao publicar usando uma ferramenta como SQLCMD.EXE.
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|Essa configuração dita como a ordenação do banco de dados é tratada durante a implantação; por padrão, a ordenação do banco de dados de destino será atualizada se não corresponder à ordenação especificada pela origem. Quando essa opção estiver configurada, a ordenação do banco de dados de destino (ou do servidor) deverá ser usada.|
|**/p:**|CreateNewDatabase=(BOOLEAN)|Especifica se o banco de dados de destino deve ser atualizado ou removido e recriado quando um banco de dados é publicado.
|**/p:**|DatabaseEdition = ({Basic&#124;Standard&#124;Premium&#124;padrão} 'Default')|Define a edição de um banco de dados do SQL Azure.
|**/p:**|DatabaseMaximumSize=(INT32)|Define o tamanho máximo, em GB, de um Banco de Dados SQL do Azure.
|**/p:**|DatabaseServiceObjective=(STRING)|Define o nível de desempenho de um Banco de Dados SQL do Azure, assim como "P0" ou "S1".
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|Se for verdadeiro, o banco de dados será definido como o Modo de Usuário Único antes da implantação.
|**/p:**|DisableAndReenableDdlTriggers = (BOOLIANO ' True')| Especifica se os gatilhos da DDL (linguagem de definição de dados) são desabilitados no início do processo de publicação e reabilitados no final da ação de publicação.|
|**/p:**|DoNotAlterChangeDataCaptureObjects = (BOOLIANO ' True')|Se for verdadeiro, os objetos do Change Data Capture não serão alterados.
|**/p:**|DoNotAlterReplicatedObjects = (BOOLIANO ' True')|Especifica se os objetos que forem replicados são identificados durante a verificação.
|**/p:**|DoNotDropObjectType=(STRING)|Um tipo de objeto que não deve ser descartado quando DropObjectsNotInSource está definido como true. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.
|**/p:**|DoNotDropObjectTypes=(STRING)|Uma lista separada por ponto e vírgula de tipos de objeto que não devem ser removidos quando DropObjectsNotInSource é true. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.
|**/p:**|DropConstraintsNotInSource = (BOOLIANO ' True')|Especifica se as restrições que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você em um banco de dados.|
|**/p:**|DropDmlTriggersNotInSource = (BOOLIANO ' True')|Especifica se gatilhos DML que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você em um banco de dados.|
|**/p:**|DropExtendedPropertiesNotInSource = (BOOLIANO ' True')|Especifica se as propriedades estendidas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropIndexesNotInSource = (BOOLIANO ' True')|Especifica se índices que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você em um banco de dados.|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|Especifica se objetos que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você em um banco de dados. Esse valor prevalece sobre DropExtendedProperties.|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|Especifica se as permissões que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|Especifica se os membros de função que não estão definidos no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropStatisticsNotInSource = (BOOLIANO ' True')|Especifica se as estatísticas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você em um banco de dados.|
|**/p:**|ExcludeObjectType=(STRING)|Um tipo de objeto que deve ser ignorado durante a implantação. Os nomes de tipo de objeto válidos são Agregações, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificados, ColumnEncryptionKeys, ColumnMasterKeys, Contratos, DatabaseRoles, DatabaseTriggers, Padrões, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Grupos de arquivos, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissões, Filas, RemoteServiceBindings, RoleMembership, Regras, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequências, Serviços, Assinaturas, StoredProcedures, SymmetricKeys, Sinônimos, Tabelas, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Usuários, Exibições, XmlSchemaCollections, Auditorias, Credenciais, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Pontos de extremidade, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logons, Rotas, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.
|**/p:**|ExcludeObjectTypes=(STRING)|Uma lista, delimitada por ponto e vírgula, de tipos de objetos que devem ser ignorados durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|Automaticamente fornece um valor padrão ao atualizar uma tabela que contém dados com uma coluna que não permite valores nulos.
|**/p:**|IgnoreAnsiNulls = (BOOLIANO ' True')|Especifica se diferenças na configuração ANSI NULLS deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|Especifica se diferenças no Autorizador deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|Especifica se diferenças nas ordenações de coluna deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|Especifica se as diferenças na ordem das colunas da tabela devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|
|**/p:**|IgnoreComments=(BOOLEAN)|Especifica se diferenças nos comentários deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.
|**/p:**|IgnoreCryptographicProviderFilePath = (BOOLIANO ' True')|Especifica se as diferenças no caminho do arquivo para o provedor de criptografia deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um servidor ou banco de dados.|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|Especifica se diferenças no esquema padrão deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DML (linguagem de manipulação de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DML deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|Especifica se diferenças nas propriedades estendidas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFileAndLogFilePath = (BOOLIANO ' True')|Especifica se diferenças nos caminhos para arquivos e arquivos de log deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFilegroupPlacement = (BOOLIANO ' True')|Especifica se diferenças no posicionamento de objetos em FILEGROUPs deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFileSize = (BOOLIANO ' True')|Especifica se diferenças nos tamanhos de arquivos deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.|
|**/p:**|IgnoreFillFactor = (BOOLIANO ' True')|Especifica se diferenças no fator de preenchimento de armazenamento de índice deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar.|
|**/p:**|IgnoreFullTextCatalogFilePath = (BOOLIANO ' True')|Especifica se diferenças no caminho do arquivo para o texto completo deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|Especifica se diferenças na semente de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar atualizações em um banco de dados.|
|**/p:**|IgnoreIncrement=(BOOLEAN)|Especifica se diferenças no incremento de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|Especifica se diferenças nas opções de índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreIndexPadding = (BOOLIANO ' True')|Especifica se diferenças nas opções de preenchimento do índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreKeywordCasing = (BOOLIANO ' True')|Especifica se diferenças no uso de maiúsculas e minúsculas em palavras-chave deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|Especifica se diferenças no uso de dicas de bloqueio em índices deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreLoginSids = (BOOLIANO ' True')| Especifica se diferenças no número SID (identificação de segurança) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|Especifica se as configurações que não sejam para replicação deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme = (BOOLIANO ' True')|Especifica se o posicionamento de um objeto em um esquema de partição deverá ser ignorado ou atualizado quando você publicar em um banco de dados.|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|Especifica se diferenças em esquemas de partição e funções deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnorePermissions=(BOOLEAN)|Especifica se diferenças nas permissões deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreQuotedIdentifiers = (BOOLIANO ' True')|Especifica se diferenças na configuração de identificadores entre aspas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|Especifica se as diferenças nas associações de logons à função devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|
|**/p:**|IgnoreRouteLifetime = (BOOLIANO ' True')|Especifica se diferenças na quantidade de tempo que o SQL Server retém a rota na tabela de roteamento deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreSemicolonBetweenStatements = (BOOLIANO ' True')|Especifica se diferenças nos pontos e vírgulas entre instruções T-SQL serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|Especifica se diferenças nas opções de tabela serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|Especifica se diferenças nos objetos de configurações do usuário serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreWhitespace = (BOOLIANO ' True')|Especifica se diferenças de espaço em branco serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para restrições de verificação serão ignoradas ou atualizadas quando você publicar.|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para chaves estrangeiras serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|Inclua todos os elementos compostos como parte de uma única operação de publicação.|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|Especifica se instruções transacionais deverão ser usadas quando possível quando você publicar em um banco de dados.|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|Especifica se a publicação sempre deverá cancelar e recriar um assembly se houver uma diferença em vez de emitir uma instrução ALTER ASSEMBLY.|
|**/p:**|PopulateFilesOnFileGroups = (BOOLIANO ' True')|Especifica se um novo arquivo também será criado quando um novo FileGroup for criado no banco de dados de destino.|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|Especifica se o esquema está registrado com o servidor de banco de dados.|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|Especifica se os colaboradores de DeploymentPlanExecutor devem ser executados quando outras operações são executadas.|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|Especifica se diferenças na ordenação do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|Especifica se diferenças na compatibilidade do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|ScriptDatabaseOptions = (BOOLIANO ' True')|Especifica se as propriedades do banco de dados de destino devem ser definidas ou atualizadas como parte da ação de publicação.|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|Especifica se as instruções são geradas no script de publicação para verificar se o nome do banco de dados e o nome do servidor correspondem aos nomes especificados no projeto de banco de dados.|
|**/p:**|ScriptFileSize=(BOOLEAN)|Controla se o tamanho é especificado ao adicionar um arquivo a um grupo de arquivos.|
|**/p:**|ScriptNewConstraintValidation = (BOOLIANO ' True')|No final da publicação, todas as restrições serão verificadas em conjunto, evitando erros de dados causados por uma verificação ou uma restrição de chave estrangeira no meio da publicação. Se definido como False, as restrições serão publicadas sem verificar os dados correspondentes.|
|**/p:**|ScriptRefreshModule = (BOOLIANO ' True')|Inclua instruções de atualização no fim do script de publicação.|
|**/p:**|Armazenamento = ({arquivo&#124;memória})|Especifica como os elementos são armazenados ao criar o modelo de banco de dados. Por razões de desempenho, o padrão é InMemory. Para bancos de dados grandes, é necessário realizar armazenamento de backup de arquivos.|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|Especifica se os erros encontrados durante a publicação verificação deve ser tratada como avisos. A verificação é executada em relação ao plano de implantação gerado antes de o plano ser executado em relação ao banco de dados de destino. A verificação do plano detecta problemas, como a perda de objetos apenas de destino (por exemplo, índices), que devem ser cancelados para fazer uma alteração. A verificação também detectará situações em que existem dependências (como tabelas ou exibições) devido a uma referência a um projeto composto, mas não existem no banco de dados de destino. Você pode optar por fazer isso para obter uma lista completa de todos os problemas, em vez de ter a ação de publicação parar no primeiro erro.|
|**/p:**|UnmodifiableObjectWarnings = (BOOLIANO ' True')|Especifica se devem ser gerados avisos quando diferenças forem localizadas em objetos que não podem ser modificados, por exemplo, se o tamanho ou os caminhos de arquivo forem diferentes para um arquivo.|
|**/p:**|VerifyCollationCompatibility = (BOOLIANO ' True')|Especifica se a compatibilidade de ordenação é verificada.
|**/p:**|VerifyDeployment = (BOOLIANO ' True')|Especifica se devem ser executadas verificações antes da publicação, o que interromperá a ação de publicação se houver problemas que possam bloquear uma publicação bem-sucedida. Por exemplo, sua ação de publicação poderá ser interrompida se você tiver chaves estrangeiras no banco de dados de destino que não existem no projeto de banco de dados, o que causará erros ao publicar.|
  
