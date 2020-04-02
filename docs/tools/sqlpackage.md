---
title: SqlPackage.exe
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: pensivebrian
ms.author: broneill
ms.reviewer: alayu; sstein
ms.date: 03/17/2020
ms.openlocfilehash: 3a45b9164d2d81983e9a40f0395189979d4daa7d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79448255"
---
# <a name="sqlpackageexe"></a>SqlPackage.exe

O **SqlPackage.exe** é um utilitário de linha de comando que automatiza as seguintes tarefas de desenvolvimento de banco de dados:  
  
- [Extrair](#help-for-the-extract-action): cria um arquivo (.dacpac) de instantâneo de um banco de dados do SQL Server dinâmico ou do Banco de Dados SQL do Azure.  
  
- [Publicar](#publish-parameters-properties-and-sqlcmd-variables): atualiza um esquema de banco de dados incrementalmente para que corresponda ao esquema de um arquivo .dacpac de origem. Se o banco de dados não existir no servidor, a operação de publicação irá criá-lo. Caso contrário, um banco de dados existente é atualizado.  
  
- [Export](#export-parameters-and-properties): exporta um banco de dados dinâmico – incluindo o esquema e os dados de usuário do banco de dados – do SQL Server ou do Banco de Dados SQL do Azure para um pacote BACPAC (arquivo .bacpac).  
  
- [Import](#import-parameters-and-properties): importa os dados de esquema e tabela de um pacote BACPAC para um novo banco de dados do usuário em uma instância do SQL Server ou do Banco de Dados SQL do Azure.  
  
- [DeployReport](#deployreport-parameters-and-properties): cria um relatório XML das alterações que teriam sido feitas por uma ação de publicação.  
  
- [DriftReport](#driftreport-parameters): cria um relatório XML das alterações que teriam sido feitas a um banco de dados registrado desde o último registro.  
  
- [Script](#script-parameters-and-properties): cria um script de atualização incremental Transact-SQL que atualiza o esquema de um destino para que corresponda ao esquema de origem.  
  
A linha de comando do **SqlPackage.exe** permite que você especifique essas ações junto com parâmetros e propriedades específicos da ação.  

**[Baixe a versão mais recente](sqlpackage-download.md)** . Para obter detalhes sobre a versão mais recente, confira as [notas sobre a versão](release-notes-sqlpackage.md).
  
## <a name="command-line-syntax"></a>Sintaxe da linha de comando

O **SqlPackage.exe** inicia as ações especificadas usando os parâmetros, as propriedades e as variáveis SQLCMD especificados na linha de comando.  
  
```
SqlPackage {parameters}{properties}{SQLCMD Variables}  
```

### <a name="usage-examples"></a>Exemplos de uso

**Gerar uma comparação entre bancos de dados usando arquivos .dacpac com uma saída do script SQL**

Comece criando um arquivo .dacpac das alterações mais recentes do banco de dados:

```
sqlpackage.exe /TargetFile:"C:\sqlpackageoutput\output_current_version.dacpac" /Action:Extract /SourceServerName:"." /SourceDatabaseName:"Contoso.Database"
 ```
 
Crie um arquivo .dacpac do destino do banco de dados (que não tem alterações):

 ```
 sqlpackage.exe /TargetFile:"C:\sqlpackageoutput\output_target.dacpac" /Action:Extract /SourceServerName:"." /SourceDatabaseName:"Contoso.Database"
 ```

Crie um script SQL que gera as diferenças de dois arquivos .dacpac:

```
sqlpackage.exe /Action:Script /SourceFile:"C:\sqlpackageoutput\output_current_version.dacpac" /TargetFile:"C:\sqlpackageoutput\output_target.dacpac" /TargetDatabaseName:"Contoso.Database" /OutputPath:"C:\sqlpackageoutput\output.sql"
 ```

### <a name="help-for-the-extract-action"></a>Ajuda para a ação Extrair

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Extract|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação; {NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action:Extract /?. |
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão. |
|**/SourceConnectionString:**|**/scs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/sdn**|{string}|Define o nome do banco de dados de origem. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo SSL a ser usado para criptografar a conexão de banco de dados de origem e ignorar a verificação cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/TargetFile:**|**/tf**|{string}| Especifica um arquivo de destino (ou seja, um arquivo .dacpac) a ser usado como destino da ação em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de destino será válido. Esse parâmetro será inválido para ações que dão suporte apenas a destinos de banco de dados.| 
|**/TenantId:**|**/tid**|{string}|Representa o nome de domínio ou a ID do locatário do Azure AD. Essa opção é necessária para dar suporte a usuários convidados ou importados do Azure AD e a contas Microsoft, como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário padrão do Azure AD será usada, supondo que o usuário autenticado seja um usuário nativo desse AD. No entanto, nesse caso, não há suporte para usuários convidados ou importados e/ou contas da Microsoft hospedadas nesse Azure AD, e a operação falhará. <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação universal deve ser usada. Quando definido como True, o protocolo de autenticação interativo é ativado para dar suporte a MFA (autenticação multifator). Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo que exige que o usuário digite seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication está definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/scs). Quando /UniversalAuthentication está definido como False, a autenticação do Azure AD deve ser especificada em SourceConnectionString (/scs). <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|

### <a name="properties-specific-to-the-extract-action"></a>Propriedades específicas da ação Extrair

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.|
|**/p:**|DacApplicationDescription=(STRING)|Define a descrição do aplicativo a ser armazenada nos metadados do DACPAC.|
|**/p:**|DacApplicationName=(STRING)|Definiu o nome do aplicativo a ser armazenado nos metadados do DACPAC. O valor padrão é o nome do banco de dados.|
|**/p:**|DacMajorVersion=(INT32 '1')|Define a versão principal a ser armazenada nos metadados do DACPAC.|
|**/p:**|DacMinorVersion=(INT32 '0')|Define a versão secundária a ser armazenada nos metadados do DACPAC.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| Especifica o tempo limite de bloqueio do banco de dados em segundos ao executar consultas em SQL Server. Use -1 para esperar indefinidamente.|
|**/p:**|ExtractAllTableData=(BOOLEAN)|Indica se os dados de todas as tabelas de usuários são extraídos. Se "true", os dados de todas as tabelas de usuários serão extraídos, e você não poderá especificar tabelas de usuários individuais para extrair dados. Se "false", especifique uma ou mais tabelas de usuário para extrair dados.|
|**/p:**|ExtractApplicationScopedObjectsOnly=(BOOLEAN 'True')|Se for verdadeiro, apenas extrairá objetos com escopo para o aplicativo da origem especificada. Se for falso, extrairá todos os objetos com escopo para o aplicativo da origem especificada.|
|**/p:**|ExtractReferencedServerScopedElements=(BOOLEAN 'True')|Se true, extrairá logon, auditoria de servidor e objetos de credencial referenciados pelos objetos do banco de dados de origem.|
|**/p:**|ExtractUsageProperties=(BOOLEAN)|Especifica se propriedades de uso, como contagem de linhas da tabela e tamanho do índice, serão extraídas do banco de dados.|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|Especifica se as propriedades estendidas devem ser ignoradas.|
|**/p:**|IgnorePermissions=(BOOLEAN 'True')|Especifica se as permissões devem ser ignoradas.|
|**/p:**|IgnoreUserLoginMappings=(BOOLEAN)|Especifica se os relacionamentos entre usuários e logons devem ser ignorados.|
|**/p:**|LongRunningCommandTimeout=(INT32)| Especifica o tempo limite do comando de execução prolongada em segundos ao executar consultas com relação ao SQL Server. Use 0 para esperar indefinidamente.|
|**/p:**|Storage=({File&#124;Memory} 'File')|Especifica o tipo de armazenamento de backup para o modelo de esquema usado durante a extração.|
|**/p:**|TableData=(STRING)|Indica a tabela a partir da qual os dados serão extraídos. Especifique o nome da tabela com ou sem os colchetes ao redor das partes do nome no seguinte formato: nome_esquema.identificador_tabela. Essa opção pode ser especificada várias vezes.|
|**/p:**| TempDirectoryForTableData=(STRING)|Especifica o diretório temporário usado para armazenar em buffer os dados da tabela antes de serem gravados no arquivo do pacote.|
|**/p:**|VerifyExtraction=(BOOLEAN)|Especifica se o dacpac extraído deve ser verificado.|

## <a name="publish-parameters-properties-and-sqlcmd-variables"></a>Parâmetro, propriedades e variáveis SQLCMD de publicação

Uma operação de publicação SqlPackage.exe atualiza o esquema de um banco de dados de destino incrementalmente para que corresponda à estrutura de um banco de dados de origem. A publicação de um pacote de implantação que contenha dados de usuário para todos ou para um subconjunto das tabelas atualizará os dados da tabela além do esquema. A implantação de dados substitui o esquema e os dados em tabelas existentes do banco de dados de destino. A implantação de dados não alterará o esquema existente ou os dados no banco de dados de destino para tabelas que não são incluídas no pacote de implantação.  

### <a name="help-for-publish-action"></a>Ajuda para a ação Publicar

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Publicar|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/AzureKeyVaultAuthMethod:**|**/akv**|{Interactive&#124;ClientIdSecret}|Especifica o método de autenticação que é usado para acessar o Azure Key Vault |
|**/ClientId:**|**/cid**|{string}|Especifica a ID do Cliente a ser usada na autenticação no Azure Key Vault, quando necessário |
|**/DeployScriptPath:**|**/dsp**|{string}|Especifica um caminho de arquivo opcional no qual o script de implantação será salvo. Nas implantações do Azure, se houver comandos TSQL para criar ou banco de dados mestre para modificar, um script será gravado no mesmo caminho, mas com "Filename_Master.sql" como o nome do arquivo de saída. |
|**/DeployReportPath:**|**/drp**|{string}|Especifica um caminho de arquivo opcional no qual o arquivo xml do relatório de implantação será salvo. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Profile:**|**/pr**|{string}|Especifica o caminho de um arquivo para um perfil de publicação do DAC. O perfil define uma coleção de propriedades e variáveis para serem usadas ao gerar saídas.|
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação;{NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action:Publish /?.|
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/Secret:**|**/secr**|{string}|Especifica o Segredo do Cliente a ser usado na autenticação no Azure Key Vault, quando necessário |
|**/SourceConnectionString:**|**/scs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/sdn**|{string}|Define o nome do banco de dados de origem. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/SourceFile:**|**/sf**|{string}|Especifica um arquivo de origem a ser usado como origem da ação, em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de origem deverá ser válido. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo SSL a ser usado para criptografar a conexão de banco de dados de origem e ignorar a verificação cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/TargetConnectionString:**|**/tcs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. No Azure AD, recomendamos que esse valor seja maior ou igual a 30 segundos.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se SSL será usado para criptografar a conexão de banco de dados de destino e ignorar a cadeia de certificados para validar a confiança. |
|**/TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de domínio ou a ID do locatário do Azure AD. Essa opção é necessária para dar suporte a usuários convidados ou importados do Azure AD e a contas Microsoft, como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário padrão do Azure AD será usada, supondo que o usuário autenticado seja um usuário nativo desse AD. No entanto, nesse caso, não há suporte para usuários convidados ou importados e/ou contas da Microsoft hospedadas nesse Azure AD, e a operação falhará. <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação universal deve ser usada. Quando definido como True, o protocolo de autenticação interativo é ativado para dar suporte a MFA (autenticação multifator). Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo que exige que o usuário digite seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication está definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/scs). Quando /UniversalAuthentication está definido como False, a autenticação do Azure AD deve ser especificada em SourceConnectionString (/scs). <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/Variables:**|**/v**|{PropertyName}={Value}|Especifica um par nome-valor para uma variável específica de ação;{NomeDaVariável}={Valor}. O arquivo DACPAC contém a lista de variáveis SQLCMD válidas. Ocorrerá um erro se não for fornecido um valor para cada variável. |

### <a name="properties-specific-to-the-publish-action"></a>Propriedades específicas da ação Publicar

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|Especifica argumentos adicionais de colaborador de implantação para os colaboradores de implantação. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula.|
|**/p:**|AdditionalDeploymentContributors=(STRING)|Especifica colaboradores adicionais de implantação que devem ser executados quando o DACPAC é implantado. Ele deve ser em formato de lista delimitada por ponto e vírgula com os IDs ou nomes totalmente qualificados do colaborador de compilação.|
|**/p:**|AdditionalDeploymentContributorPaths=(STRING)| Especifica caminhos para carregar colaboradores de implantação adicionais. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula. | 
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|Essa propriedade é usada pela implantação de SqlClr para descartar os assemblies com bloqueio como parte do plano de implantação. Por padrão, os assemblies de bloqueio/referência bloquearão uma atualização de assembly se o assembly de referência precisar ser descartado.|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|Especifica se a ação deve continuar apesar de plataformas do SQL Server potencialmente incompatíveis.|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|Não bloqueie a movimentação de dados em uma tabela que tenha Segurança em Nível de Linha se essa propriedade estiver definida como true. O padrão é false.|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|Faz backups do banco de dados antes de implantar qualquer alteração.|
|**/p:**|BlockOnPossibleDataLoss=(BOOLEAN 'True')|Especifica que o episódio de publicação deverá ser terminado se houver uma possibilidade de perda de dados resultante da operação de publicação.|
|**/p:**|BlockWhenDriftDetected=(BOOLEAN 'True')|Especifica se deve bloquear a atualização de um banco de dados cujo esquema não mais corresponda seu registro ou não esteja registrado.|
|**/p:**|CommandTimeout=(INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.|
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|Especifica se a declaração de variáveis SETVAR devem ser comentadas no script de publicação gerado. Você pode optar por fazer isso se planejar especificar os valores na linha de comando ao publicar usando uma ferramenta como SQLCMD.EXE.|
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|Essa configuração dita como a ordenação do banco de dados é tratada durante a implantação; por padrão, a ordenação do banco de dados de destino será atualizada se não corresponder à ordenação especificada pela origem. Quando essa opção estiver configurada, a ordenação do banco de dados de destino (ou do servidor) deverá ser usada.|
|**/p:**|CreateNewDatabase=(BOOLEAN)|Especifica se o banco de dados de destino deve ser atualizado ou removido e recriado quando um banco de dados é publicado.|
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Define a edição de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')|Especifica o tempo limite de bloqueio do banco de dados em segundos ao executar consultas em SQL Server. Use -1 para esperar indefinidamente.|
|**/p:**|DatabaseMaximumSize=(INT32)|Define o tamanho máximo, em GB, de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseServiceObjective=(STRING)|Define o nível de desempenho de um Banco de Dados SQL do Azure, como "P0" ou "S1".|
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|Se for verdadeiro, o banco de dados será definido como o Modo de Usuário Único antes da implantação.|
|**/p:**|DisableAndReenableDdlTriggers=(BOOLEAN 'True')|Especifica se os gatilhos da DDL (linguagem de definição de dados) são desabilitados no início do processo de publicação e reabilitados no final da ação de publicação.|
|**/p:**|DoNotAlterChangeDataCaptureObjects=(BOOLEAN 'True')|Se for verdadeiro, os objetos do Change Data Capture não serão alterados.|
|**/p:**|DoNotAlterReplicatedObjects=(BOOLEAN 'True')|Especifica se os objetos que forem replicados são identificados durante a verificação.|
|**/p:**|DoNotDropObjectType=(STRING)|Um tipo de objeto que não deve ser descartado quando DropObjectsNotInSource é verdadeiro. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|DoNotDropObjectTypes=(STRING)|Uma lista separada por ponto e vírgula de tipos de objeto que não devem ser removidos quando DropObjectsNotInSource é true. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|DropConstraintsNotInSource=(BOOLEAN 'True')|Especifica se as restrições que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropDmlTriggersNotInSource=(BOOLEAN 'True')|Especifica se os gatilhos DML que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publica em um banco de dados.|
|**/p:**|DropExtendedPropertiesNotInSource=(BOOLEAN 'True')|Especifica se as propriedades estendidas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropIndexesNotInSource=(BOOLEAN 'True')|Especifica se os índices que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|Especifica se os objetos que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar em um banco de dados. Esse valor tem precedência sobre DropExtendedProperties.|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|Especifica se as permissões que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|Especifica se os membros de função que não estão definidos no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropStatisticsNotInSource=(BOOLEAN 'True')|Especifica se as estatísticas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|ExcludeObjectType=(STRING)|Um tipo de objeto que deve ser ignorado durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|ExcludeObjectTypes=(STRING)|Uma lista, delimitada por ponto e vírgula, de tipos de objetos que devem ser ignorados durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|Automaticamente fornece um valor padrão ao atualizar uma tabela que contém dados com uma coluna que não permite valores nulos.|
|**/p:**|IgnoreAnsiNulls=(BOOLEAN 'True')|Especifica se diferenças na configuração ANSI NULLS deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|Especifica se diferenças no Autorizador deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|Especifica se diferenças nas ordenações de coluna deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|Especifica se as diferenças na ordem das colunas da tabela devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|
|**/p:**|IgnoreComments=(BOOLEAN)|Especifica se diferenças nos comentários deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreCryptographicProviderFilePath=(BOOLEAN 'True')|Especifica se as diferenças no caminho do arquivo para o provedor de criptografia deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um servidor ou banco de dados.|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|Especifica se diferenças no esquema padrão deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DML (linguagem de manipulação de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DML deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|Especifica se diferenças nas propriedades estendidas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFileAndLogFilePath=(BOOLEAN 'True')|Especifica se diferenças nos caminhos para arquivos e arquivos de log deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFilegroupPlacement=(BOOLEAN 'True')|Especifica se diferenças no posicionamento de objetos em FILEGROUPs deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFileSize=(BOOLEAN 'True')|Especifica se diferenças nos tamanhos de arquivos deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.|
|**/p:**|IgnoreFillFactor=(BOOLEAN 'True')|Especifica se diferenças no fator de preenchimento de armazenamento de índice deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.|
|**/p:**|IgnoreFullTextCatalogFilePath=(BOOLEAN 'True')|Especifica se diferenças no caminho do arquivo do catálogo de texto completo deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|Especifica se diferenças na semente de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar atualizações em um banco de dados.|
|**/p:**|IgnoreIncrement=(BOOLEAN)|Especifica se diferenças no incremento de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|Especifica se diferenças nas opções de índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreIndexPadding=(BOOLEAN 'True')|Especifica se diferenças nas opções de preenchimento do índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreKeywordCasing=(BOOLEAN 'True')|Especifica se diferenças no uso de maiúsculas e minúsculas em palavras-chave deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|Especifica se diferenças no uso de dicas de bloqueio em índices deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreLoginSids=(BOOLEAN 'True')|Especifica se diferenças no número SID (identificação de segurança) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|Especifica se as configurações que não sejam para replicação deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme=(BOOLEAN 'True')|Especifica se o posicionamento de um objeto em um esquema de partição deverá ser ignorado ou atualizado quando você publicar em um banco de dados.|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|Especifica se diferenças em esquemas de partição e funções deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnorePermissions=(BOOLEAN)|Especifica se diferenças nas permissões deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreQuotedIdentifiers=(BOOLEAN 'True')|Especifica se diferenças na configuração de identificadores entre aspas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|Especifica se as diferenças nas associações de logons à função devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|
|**/p:**|IgnoreRouteLifetime=(BOOLEAN 'True')|Especifica se diferenças na quantidade de tempo que o SQL Server retém a rota na tabela de roteamento deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreSemicolonBetweenStatements=(BOOLEAN 'True')|Especifica se diferenças nos pontos e vírgulas entre instruções T-SQL serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|Especifica se diferenças nas opções de tabela serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreTablePartitionOptions=(BOOLEAN)|Especifica se diferenças nas opções de partição de tabela serão ignoradas ou atualizadas quando você publicar em um banco de dados.  Essa opção se aplica somente a bancos de dados (data warehouse) do pool de SQL do Azure Synapse Analytics.|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|Especifica se diferenças nos objetos de configurações do usuário serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreWhitespace=(BOOLEAN 'True')|Especifica se diferenças de espaço em branco serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para restrições de verificação serão ignoradas ou atualizadas quando você publicar.|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para chaves estrangeiras serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|Inclua todos os elementos compostos como parte de uma única operação de publicação.|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|Especifica se instruções transacionais deverão ser usadas quando possível quando você publicar em um banco de dados.|
|**/p:**|LongRunningCommandTimeout=(INT32)|Especifica o tempo limite do comando de execução prolongada em segundos ao executar consultas com relação ao SQL Server. Use 0 para esperar indefinidamente.|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|Especifica se a publicação sempre deverá cancelar e recriar um assembly se houver uma diferença em vez de emitir uma instrução ALTER ASSEMBLY.|
|**/p:**|PopulateFilesOnFileGroups=(BOOLEAN 'True')|Especifica se um novo arquivo também será criado quando um novo FileGroup for criado no banco de dados de destino.|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|Especifica se o esquema está registrado com o servidor de banco de dados.|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|Especifica se os colaboradores de DeploymentPlanExecutor devem ser executados quando outras operações forem executadas.|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|Especifica se diferenças na ordenação do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|Especifica se diferenças na compatibilidade do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|ScriptDatabaseOptions=(BOOLEAN 'True')|Especifica se as propriedades do banco de dados de destino devem ser definidas ou atualizadas como parte da ação de publicação.|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|Especifica se as instruções são geradas no script de publicação para verificar se o nome do banco de dados e o nome do servidor correspondem aos nomes especificados no projeto de banco de dados.|
|**/p:**|ScriptFileSize=(BOOLEAN)|Controla se o tamanho é especificado ao adicionar um arquivo a um grupo de arquivos.|
|**/p:**|ScriptNewConstraintValidation=(BOOLEAN 'True')|No final da publicação, todas as restrições serão verificadas em conjunto, evitando erros de dados causados por uma verificação ou restrição de chave estrangeira no meio da publicação. Se definido como False, as restrições serão publicadas sem verificar os dados correspondentes.|
|**/p:**|ScriptRefreshModule=(BOOLEAN 'True')|Inclua instruções de atualização no fim do script de publicação.|
|**/p:**|Storage=({File&#124;Memory})|Especifica como os elementos são armazenados ao criar o modelo de banco de dados. Por razões de desempenho, o padrão é InMemory. Para bancos de dados grandes, é necessário realizar armazenamento de backup de arquivos.|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|Especifica se os erros encontrados durante a verificação de publicação devem ser tratados como avisos. A verificação é executada em relação ao plano de implantação gerado antes de o plano ser executado em relação ao banco de dados de destino. A verificação do plano detecta problemas, como a perda de objetos apenas de destino (por exemplo, índices), que devem ser cancelados para fazer uma alteração. A verificação também detectará situações em que existem dependências (como tabelas ou exibições) devido a uma referência a um projeto composto, mas não existem no banco de dados de destino. Você pode optar por fazer isso para obter uma lista completa de todos os problemas, em vez de interromper a ação de publicação no primeiro erro.
|**/p:**|UnmodifiableObjectWarnings=(BOOLEAN 'True')|Especifica se devem ser gerados avisos quando diferenças forem localizadas em objetos que não podem ser modificados, por exemplo, se o tamanho ou os caminhos de arquivo forem diferentes para um arquivo.|
|**/p:**|VerifyCollationCompatibility=(BOOLEAN 'True')|Especifica se a compatibilidade de ordenação é verificada.|
|**/p:**|VerifyDeployment=(BOOLEAN 'True')|Especifica se devem ser executadas verificações antes da publicação, o que interromperá a ação de publicação se houver problemas que possam bloquear uma publicação bem-sucedida. Por exemplo, sua ação de publicação poderá ser interrompida se você tiver chaves estrangeiras no banco de dados de destino que não existem no projeto de banco de dados, o que causará erros ao publicar.|
|

### <a name="sqlcmd-variables"></a>Variáveis SQLCMD

A tabela a seguir descreve o formato da opção que pode ser usada para substituir o valor de uma variável de comando SQL (**sqlcmd**) usada durante uma ação de publicação. Os valores da variável especificados na linha de comando substituem outros valores atribuídos à variável (por exemplo, em um perfil de publicação).  
  
|Parâmetro|Padrão|Descrição|  
|-------------|-----------|---------------|  
|**/Variables:{PropertyName}={Value}**||Especifica um par nome-valor para uma variável específica de ação; {NomeDaVariável}={Valor}. O arquivo DACPAC contém a lista de variáveis SQLCMD válidas. Ocorrerá um erro se não for fornecido um valor para cada variável.|  
  
## <a name="export-parameters-and-properties"></a>Parâmetros e propriedades de exportação

Uma ação de exportação SqlPackage.exe exporta um banco de dados ativo do SQL Server ou do Banco de Dados SQL do Azure para um pacote BACPAC (arquivo .bacpac). Por padrão, os dados de todas as tabelas serão incluídos no arquivo .bacpac. Como opção, você pode especificar apenas um subconjunto das tabelas para o qual exportará dados. A validação para a ação Exportar garante a compatibilidade do Banco de Dados SQL do Azure para o banco de dados de destino completo, mesmo que esteja especificado um subconjunto das tabelas para a exportação.  
  
### <a name="help-for-export-action"></a>Ajuda para a ação Exportar

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Exportação|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação;{NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action:Export /?.|
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/SourceConnectionString:**|**/scs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/sdn**|{string}|Define o nome do banco de dados de origem. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo SSL a ser usado para criptografar a conexão de banco de dados de origem e ignorar a verificação cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/TargetFile:**|**/tf**|{string}| Especifica um arquivo de destino (ou seja, um arquivo .dacpac) a ser usado como destino da ação em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de destino será válido. Esse parâmetro será inválido para ações que dão suporte apenas a destinos de banco de dados.|
|**/TenantId:**|**/tid**|{string}|Representa o nome de domínio ou a ID do locatário do Azure AD. Essa opção é necessária para dar suporte a usuários convidados ou importados do Azure AD e a contas Microsoft, como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário padrão do Azure AD será usada, supondo que o usuário autenticado seja um usuário nativo desse AD. No entanto, nesse caso, não há suporte para usuários convidados ou importados e/ou contas da Microsoft hospedadas nesse Azure AD, e a operação falhará. <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação universal deve ser usada. Quando definido como True, o protocolo de autenticação interativo é ativado para dar suporte a MFA (autenticação multifator). Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo que exige que o usuário digite seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication está definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/scs). Quando /UniversalAuthentication está definido como False, a autenticação do Azure AD deve ser especificada em SourceConnectionString (/scs). <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|

### <a name="properties-specific-to-the-export-action"></a>Propriedades específicas da ação Exportar

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| Especifica o tempo limite de bloqueio do banco de dados em segundos ao executar consultas em SQL Server. Use -1 para esperar indefinidamente.|
|**/p:**|LongRunningCommandTimeout=(INT32)| Especifica o tempo limite do comando de execução prolongada em segundos ao executar consultas com relação ao SQL Server. Use 0 para esperar indefinidamente.|
|**/p:**|Storage=({File&#124;Memory} 'File')|Especifica o tipo de armazenamento de backup para o modelo de esquema usado durante a extração.|
|**/p:**|TableData=(STRING)|Indica a tabela a partir da qual os dados serão extraídos. Especifique o nome da tabela com ou sem os colchetes ao redor das partes do nome no seguinte formato: nome_esquema.identificador_tabela. Essa opção pode ser especificada várias vezes.|
|**/p:**|TempDirectoryForTableData=(STRING)|Especifica o diretório temporário usado para armazenar em buffer os dados da tabela antes de serem gravados no arquivo do pacote.|
|**/p:**|TargetEngineVersion=({Default&#124;Latest&#124;V11&#124;V12} 'Latest')|Especifica qual é a versão esperada do mecanismo de destino. Isso afeta se os objetos que têm suporte dos servidores de Banco de Dados SQL do Azure com recursos da V12, como tabelas com otimização de memória, são permitidos no bacpac gerado.|
|**/p:**|VerifyFullTextDocumentTypesSupported=(BOOLEAN)|Especifica se os tipos de documento de texto completo compatíveis para Banco de Dados SQL do Microsoft Azure v12 devem ser verificados.|
  
## <a name="import-parameters-and-properties"></a>Parâmetros e propriedades de importação

Uma ação de importação SqlPackage.exe importa os dados do esquema e da tabela de um pacote BACPAC – arquivo .bacpac – para um banco de dados novo ou vazio no SQL Server ou no Banco de Dados SQL do Azure. No momento da operação de importação para um banco de dados existente, o banco de dados de destino não pode conter nenhum objeto de esquema definido pelo usuário.  
  
### <a name="help-for-command-actions"></a>Ajuda para ações de comando

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Importar|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação;{NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action:Import /?.|
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/SourceFile:**|**/sf**|{string}|Especifica um arquivo de origem a ser usado como a origem da ação. Se esse parâmetro for usado, nenhum outro parâmetro de origem deverá ser válido. |
|**/TargetConnectionString:**|**/tcs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. No Azure AD, recomendamos que esse valor seja maior ou igual a 30 segundos.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se SSL será usado para criptografar a conexão de banco de dados de destino e ignorar a cadeia de certificados para validar a confiança. |
|**/TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de domínio ou a ID do locatário do Azure AD. Essa opção é necessária para dar suporte a usuários convidados ou importados do Azure AD e a contas Microsoft, como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário padrão do Azure AD será usada, supondo que o usuário autenticado seja um usuário nativo desse AD. No entanto, nesse caso, não há suporte para usuários convidados ou importados e/ou contas da Microsoft hospedadas nesse Azure AD, e a operação falhará. <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação universal deve ser usada. Quando definido como True, o protocolo de autenticação interativo é ativado para dar suporte a MFA (autenticação multifator). Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo que exige que o usuário digite seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication está definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/scs). Quando /UniversalAuthentication está definido como False, a autenticação do Azure AD deve ser especificada em SourceConnectionString (/scs). <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|

Propriedades específicas da ação Importar:

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.|
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Define a edição de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| Especifica o tempo limite de bloqueio do banco de dados em segundos ao executar consultas em SQL Server. Use -1 para esperar indefinidamente.|
|**/p:**|DatabaseMaximumSize=(INT32)|Define o tamanho máximo, em GB, de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseServiceObjective=(STRING)|Define o nível de desempenho de um Banco de Dados SQL do Azure, como "P0" ou "S1".|
|**/p:**|ImportContributorArguments=(STRING)|Especifica argumentos de colaborador de implantação para os colaboradores de implantação. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula.|
|**/p:**|ImportContributors=(STRING)|Especifica que colaboradores da implantação devem ser executados quando o bacpac for importado. Ele deve ser em formato de lista delimitada por ponto e vírgula com os IDs ou nomes totalmente qualificados do colaborador de compilação.|
|**/p:**|ImportContributorPaths=(STRING)|Especifica caminhos para carregar colaboradores de implantação adicionais. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula. |
|**/p:**|LongRunningCommandTimeout=(INT32)| Especifica o tempo limite do comando de execução prolongada em segundos ao executar consultas com relação ao SQL Server. Use 0 para esperar indefinidamente.|
|**/p:**|Storage=({File&#124;Memory})|Especifica como os elementos são armazenados ao criar o modelo de banco de dados. Por razões de desempenho, o padrão é InMemory. Para bancos de dados grandes, é necessário realizar armazenamento de backup de arquivos.|
  
## <a name="deployreport-parameters-and-properties"></a>Parâmetros e propriedades de DeployReport

Uma ação de relatório do **SqlPackage.exe** cria um relatório XML das alterações que teriam sido feitas por uma ação de publicação.  
  
### <a name="help-for-deployreport-action"></a>Ajuda para a ação DeployReport

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|DeployReport|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/OutputPath:**|**/op**|{string}|Especifica o caminho de arquivo onde os arquivos de saída são gerados. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Profile:**|**/pr**|{string}|Especifica o caminho de um arquivo para um perfil de publicação do DAC. O perfil define uma coleção de propriedades e variáveis para serem usadas ao gerar saídas. |
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação; {NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action:DeployReport /?. |
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão. |
|**/SourceConnectionString:**|**/scs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/sdn**|{string}|Define o nome do banco de dados de origem. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/SourceFile:**|**/sf**|{string}|Especifica um arquivo de origem a ser usado como origem da ação, em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de origem deverá ser válido. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo SSL a ser usado para criptografar a conexão de banco de dados de origem e ignorar a verificação cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/TargetConnectionString:**|**/tcs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/TargetFile:**|**/tf**|{string}|Especifica um arquivo de destino (ou seja, um arquivo .dacpac) a ser usado como destino da ação em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de destino será válido. Esse parâmetro será inválido para ações que dão suporte apenas a destinos de banco de dados.|
|**/TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. No Azure AD, recomendamos que esse valor seja maior ou igual a 30 segundos.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se SSL será usado para criptografar a conexão de banco de dados de destino e ignorar a cadeia de certificados para validar a confiança. |
|**/TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de domínio ou a ID do locatário do Azure AD. Essa opção é necessária para dar suporte a usuários convidados ou importados do Azure AD e a contas Microsoft, como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário padrão do Azure AD será usada, supondo que o usuário autenticado seja um usuário nativo desse AD. No entanto, nesse caso, não há suporte para usuários convidados ou importados e/ou contas da Microsoft hospedadas nesse Azure AD, e a operação falhará. <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação universal deve ser usada. Quando definido como True, o protocolo de autenticação interativo é ativado para dar suporte a MFA (autenticação multifator). Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo que exige que o usuário digite seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication está definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/scs). Quando /UniversalAuthentication está definido como False, a autenticação do Azure AD deve ser especificada em SourceConnectionString (/scs). <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/Variables:**|**/v**|{PropertyName}={Value}|Especifica um par nome-valor para uma variável específica de ação; {NomeDaVariável}={Valor}. O arquivo DACPAC contém a lista de variáveis SQLCMD válidas. Ocorrerá um erro se não for fornecido um valor para cada variável. |

## <a name="properties-specific-to-the-deployreport-action"></a>Propriedades específicas da ação DeployReport

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|Especifica argumentos adicionais de colaborador de implantação para os colaboradores de implantação. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula.|
|**/p:**|AdditionalDeploymentContributors=(STRING)|Especifica colaboradores adicionais de implantação que devem ser executados quando o DACPAC é implantado. Ele deve ser em formato de lista delimitada por ponto e vírgula com os IDs ou nomes totalmente qualificados do colaborador de compilação.|
|**/p:**|AdditionalDeploymentContributorPaths=(STRING)| Especifica caminhos para carregar colaboradores de implantação adicionais. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula. | 
|**/p:**|AllowDropBlocking Assemblies=(BOOLEAN)|Essa propriedade é usada pela implantação de SqlClr para descartar os assemblies com bloqueio como parte do plano de implantação. Por padrão, os assemblies de bloqueio/referência bloquearão uma atualização de assembly se o assembly de referência precisar ser descartado.|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|Especifica se a ação deve continuar apesar de plataformas do SQL Server potencialmente incompatíveis.|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|Não bloqueie a movimentação de dados em uma tabela que tenha Segurança em Nível de Linha se essa propriedade estiver definida como true. O padrão é false.|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|Faz backups do banco de dados antes de implantar qualquer alteração.|
|**/p:**|BlockOnPossibleDataLoss=(BOOLEAN 'True')|Especifica que o episódio de publicação deverá ser terminado se houver uma possibilidade de perda de dados resultante da operação de publicação.|
|**/p:**|BlockWhenDriftDetected=(BOOLEAN 'True')|Especifica se deve bloquear a atualização de um banco de dados cujo esquema não mais corresponda seu registro ou não esteja registrado. |
|**/p:**|CommandTimeout=(INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server. |
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|Especifica se a declaração de variáveis SETVAR devem ser comentadas no script de publicação gerado. Você pode optar por fazer isso se planejar especificar os valores na linha de comando ao publicar usando uma ferramenta como SQLCMD.EXE. |
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|Essa configuração dita como a ordenação do banco de dados é tratada durante a implantação; por padrão, a ordenação do banco de dados de destino será atualizada se não corresponder à ordenação especificada pela origem. Quando essa opção estiver configurada, a ordenação do banco de dados de destino (ou do servidor) deverá ser usada. |
|**/p:**|CreateNewDatabase=(BOOLEAN)|Especifica se o banco de dados de destino deve ser atualizado ou removido e recriado quando um banco de dados é publicado. |
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Define a edição de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| Especifica o tempo limite de bloqueio do banco de dados em segundos ao executar consultas em SQL Server. Use -1 para esperar indefinidamente.|
|**/p:**|DatabaseMaximumSize=(INT32)|Define o tamanho máximo, em GB, de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseServiceObjective=(STRING)|Define o nível de desempenho de um Banco de Dados SQL do Azure, assim como "P0" ou "S1". |
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|Se for verdadeiro, o banco de dados será definido como o Modo de Usuário Único antes da implantação. |
|**/p:**|DisableAndReenableDdlTriggers=(BOOLEAN 'True')| Especifica se os gatilhos da DDL (linguagem de definição de dados) são desabilitados no início do processo de publicação e reabilitados no final da ação de publicação.|
|**/p:**|DoNotAlterChangeDataCaptureObjects=(BOOLEAN 'True')|Se for verdadeiro, os objetos do Change Data Capture não serão alterados.|
|**/p:**|DoNotAlterReplicatedObjects=(BOOLEAN 'True')|Especifica se os objetos que forem replicados são identificados durante a verificação.|
|**/p:**|DoNotDropObjectType=(STRING)|Um tipo de objeto que não deve ser descartado quando DropObjectsNotInSource é verdadeiro. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers. |
|**/p:**|DoNotDropObjectTypes=(STRING)|Uma lista separada por ponto e vírgula de tipos de objeto que não devem ser removidos quando DropObjectsNotInSource é true. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|DropConstraintsNotInSource=(BOOLEAN 'True')|Especifica se as restrições que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropDmlTriggersNotInSource=(BOOLEAN 'True')|Especifica se os gatilhos DML que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publica em um banco de dados.|
|**/p:**|DropExtendedPropertiesNotInSource=(BOOLEAN 'True')|Especifica se as propriedades estendidas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropIndexesNotInSource=(BOOLEAN 'True')|Especifica se os índices que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|Especifica se os objetos que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar em um banco de dados. Esse valor tem precedência sobre DropExtendedProperties.|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|Especifica se as permissões que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|Especifica se os membros de função que não estão definidos no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropStatisticsNotInSource=(BOOLEAN 'True')|Especifica se as estatísticas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|ExcludeObjectType=(STRING)|Um tipo de objeto que deve ser ignorado durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|ExcludeObjectTypes=(STRING)|Uma lista, delimitada por ponto e vírgula, de tipos de objetos que devem ser ignorados durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|Automaticamente fornece um valor padrão ao atualizar uma tabela que contém dados com uma coluna que não permite valores nulos.|
|**/p:**|IgnoreAnsiNulls=(BOOLEAN 'True')|Especifica se diferenças na configuração ANSI NULLS deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|Especifica se diferenças no Autorizador deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|Especifica se diferenças nas ordenações de coluna deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|Especifica se as diferenças na ordem das colunas da tabela devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|
|**/p:**|IgnoreComments=(BOOLEAN)|Especifica se diferenças nos comentários deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreCryptographicProviderFilePath=(BOOLEAN 'True')|Especifica se as diferenças no caminho do arquivo para o provedor de criptografia deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um servidor ou banco de dados.|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|Especifica se diferenças no esquema padrão deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DML (linguagem de manipulação de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DML deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|Especifica se diferenças nas propriedades estendidas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreFileAndLogFilePath=(BOOLEAN 'True')|Especifica se diferenças nos caminhos para arquivos e arquivos de log deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreFilegroupPlacement=(BOOLEAN 'True')|Especifica se diferenças no posicionamento de objetos em FILEGROUPs deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreFileSize=(BOOLEAN 'True')|Especifica se diferenças nos tamanhos de arquivos deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados. |
|**/p:**|IgnoreFillFactor=(BOOLEAN 'True')|Especifica se diferenças no fator de preenchimento de armazenamento de índice deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados|
|**/p:**|IgnoreFullTextCatalogFilePath=(BOOLEAN 'True')|Especifica se diferenças no caminho do arquivo do catálogo de texto completo deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.| 
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|Especifica se diferenças na semente de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar atualizações em um banco de dados. |
|**/p:**|IgnoreIncrement=(BOOLEAN)|Especifica se diferenças no incremento de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|Especifica se diferenças nas opções de índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreIndexPadding=(BOOLEAN 'True')|Especifica se diferenças nas opções de preenchimento do índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreKeywordCasing=(BOOLEAN 'True')|Especifica se diferenças no uso de maiúsculas e minúsculas em palavras-chave deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|Especifica se diferenças no uso de dicas de bloqueio em índices deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreLoginSids=(BOOLEAN 'True')| Especifica se diferenças no número SID (identificação de segurança) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|Especifica se as configurações que não sejam para replicação deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreObjectPlacementOnPartitionScheme=(BOOLEAN 'True')|Especifica se o posicionamento de um objeto em um esquema de partição deverá ser ignorado ou atualizado quando você publicar em um banco de dados.|
 |**/p:**|IgnorePartitionSchemes=(BOOLEAN)|Especifica se diferenças em esquemas de partição e funções deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnorePermissions=(BOOLEAN)|Especifica se diferenças nas permissões deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreQuotedIdentifiers=(BOOLEAN 'True')|Especifica se diferenças na configuração de identificadores entre aspas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|Especifica se as diferenças nas associações de logons à função devem ser ignoradas ou atualizadas quando você publica em um banco de dados. |
|**/p:**|IgnoreRouteLifetime=(BOOLEAN 'True')|Especifica se diferenças na quantidade de tempo que o SQL Server retém a rota na tabela de roteamento deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados|
|**/p:**|IgnoreSemicolonBetweenStatements=(BOOLEAN 'True')|Especifica se diferenças nos pontos e vírgulas entre instruções T-SQL serão ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreTableOptions=(BOOLEAN)|Especifica se diferenças nas opções de tabela serão ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreTablePartitionOptions=(BOOLEAN)|Especifica se diferenças nas opções de partição de tabela serão ignoradas ou atualizadas quando você publicar em um banco de dados.  Essa opção se aplica somente ao banco de dados de data warehouse do Azure Synapse Analytics.|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|Especifica se diferenças nos objetos de configurações do usuário serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreWhitespace=(BOOLEAN 'True')|Especifica se diferenças de espaço em branco serão ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para restrições de verificação serão ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para chaves estrangeiras serão ignoradas ou atualizadas quando você publicar em um banco de dados.| 
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|Inclua todos os elementos compostos como parte de uma única operação de publicação.|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|Especifica se instruções transacionais deverão ser usadas quando possível quando você publicar em um banco de dados.|
|**/p:**|LongRunningCommandTimeout=(INT32)| Especifica o tempo limite do comando de execução prolongada em segundos ao executar consultas com relação ao SQL Server. Use 0 para esperar indefinidamente.|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|Especifica se a publicação sempre deverá cancelar e recriar um assembly se houver uma diferença em vez de emitir uma instrução ALTER ASSEMBLY. |
|**/p:**|PopulateFilesOnFileGroups=(BOOLEAN 'True')|Especifica se um novo arquivo também será criado quando um novo FileGroup for criado no banco de dados de destino. |
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|Especifica se o esquema está registrado com o servidor de banco de dados. 
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|Especifica se os colaboradores de DeploymentPlanExecutor devem ser executados quando outras operações forem executadas.|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|Especifica se diferenças na ordenação do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|Especifica se diferenças na compatibilidade do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados. |
|**/p:**|ScriptDatabaseOptions=(BOOLEAN 'True')|Especifica se as propriedades do banco de dados de destino devem ser definidas ou atualizadas como parte da ação de publicação. |
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|Especifica se as instruções são geradas no script de publicação para verificar se o nome do banco de dados e o nome do servidor correspondem aos nomes especificados no projeto de banco de dados.|
|**/p:**|ScriptFileSize=(BOOLEAN)|Controla se o tamanho é especificado ao adicionar um arquivo a um grupo de arquivos. |
|**/p:**|ScriptNewConstraintValidation=(BOOLEAN 'True')|No final da publicação, todas as restrições serão verificadas em conjunto, evitando erros de dados causados por uma verificação ou restrição de chave estrangeira no meio da publicação. Se definido como False, as restrições serão publicadas sem verificar os dados correspondentes.|
|**/p:**|ScriptRefreshModule=(BOOLEAN 'True')|Inclua instruções de atualização no fim do script de publicação.|
|**/p:**|Storage=({File&#124;Memory})|Especifica como os elementos são armazenados ao criar o modelo de banco de dados. Por razões de desempenho, o padrão é InMemory. Para bancos de dados grandes, é necessário realizar armazenamento de backup de arquivos.|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|Especifica se os erros encontrados durante a verificação de publicação devem ser tratados como avisos. A verificação é executada em relação ao plano de implantação gerado antes de o plano ser executado em relação ao banco de dados de destino. A verificação do plano detecta problemas, como a perda de objetos apenas de destino (por exemplo, índices), que devem ser cancelados para fazer uma alteração. A verificação também detectará situações em que existem dependências (como tabelas ou exibições) devido a uma referência a um projeto composto, mas não existem no banco de dados de destino. Você pode optar por fazer isso para obter uma lista completa de todos os problemas, em vez de interromper a ação de publicação no primeiro erro. |
|**/p:**|UnmodifiableObjectWarnings=(BOOLEAN 'True')|Especifica se devem ser gerados avisos quando diferenças forem localizadas em objetos que não podem ser modificados, por exemplo, se o tamanho ou os caminhos de arquivo forem diferentes para um arquivo.| 
|**/p:**|VerifyCollationCompatibility=(BOOLEAN 'True')|Especifica se a compatibilidade de ordenação é verificada.| 
|**/p:**|VerifyDeployment=(BOOLEAN 'True')|Especifica se devem ser executadas verificações antes da publicação, o que interromperá a ação de publicação se houver problemas que possam bloquear uma publicação bem-sucedida. Por exemplo, sua ação de publicação poderá ser interrompida se você tiver chaves estrangeiras no banco de dados de destino que não existem no projeto de banco de dados, o que causará erros ao publicar. |
  
## <a name="driftreport-parameters"></a>Parâmetros DriftReport

Uma ação de relatório do **SqlPackage.exe** cria um relatório XML das alterações que teriam sido feitas a um banco de dados registrado desde a última vez que foi registrado.  
  
### <a name="help-for-driftreport-action"></a>Ajuda para a ação DriftReport

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|DriftReport|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/OutputPath:**|**/op**|{string}|Especifica o caminho de arquivo onde os arquivos de saída são gerados. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/TargetConnectionString:**|**/tcs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. No Azure AD, recomendamos que esse valor seja maior ou igual a 30 segundos.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se SSL será usado para criptografar a conexão de banco de dados de destino e ignorar a cadeia de certificados para validar a confiança. |
|**/TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de domínio ou a ID do locatário do Azure AD. Essa opção é necessária para dar suporte a usuários convidados ou importados do Azure AD e a contas Microsoft, como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário padrão do Azure AD será usada, supondo que o usuário autenticado seja um usuário nativo desse AD. No entanto, nesse caso, não há suporte para usuários convidados ou importados e/ou contas da Microsoft hospedadas nesse Azure AD, e a operação falhará. <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação universal deve ser usada. Quando definido como True, o protocolo de autenticação interativo é ativado para dar suporte a MFA (autenticação multifator). Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo que exige que o usuário digite seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication está definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/scs). Quando /UniversalAuthentication está definido como False, a autenticação do Azure AD deve ser especificada em SourceConnectionString (/scs). <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|

## <a name="script-parameters-and-properties"></a>Parâmetros e propriedades de script

Uma ação de script do **SqlPackage.exe** cria um script de atualização incremental Transact-SQL que atualiza o esquema de um banco de dados de destino para que corresponda ao esquema de um banco de dados de origem.  
  
### <a name="help-for-the-script-action"></a>Ajuda para a ação de Script

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Script|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/DeployScriptPath:**|**/dsp**|{string}|Especifica um caminho de arquivo opcional no qual o script de implantação será salvo. Nas implantações do Azure, se houver comandos TSQL para criar ou banco de dados mestre para modificar, um script será gravado no mesmo caminho, mas com "Filename_Master.sql" como o nome do arquivo de saída. |
|**/DeployReportPath:**|**/drp**|{string}|Especifica um caminho de arquivo opcional no qual o arquivo xml do relatório de implantação será salvo. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/OutputPath:**|**/op**|{string}|Especifica o caminho de arquivo onde os arquivos de saída são gerados. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Profile:**|**/pr**|{string}|Especifica o caminho de um arquivo para um perfil de publicação do DAC. O perfil define uma coleção de propriedades e variáveis para serem usadas ao gerar saídas.|
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação;{NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action:Script /?.|
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/SourceConnectionString:**|**/scs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/sdn**|{string}|Define o nome do banco de dados de origem. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/SourceFile:**|**/sf**|{string}|Especifica um arquivo de origem a ser usado como a origem da ação. Se esse parâmetro for usado, nenhum outro parâmetro de origem deverá ser válido. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo SSL a ser usado para criptografar a conexão de banco de dados de origem e ignorar a verificação cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/TargetConnectionString:**|**/tcs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/TargetFile:**|**/tf**|{string}| Especifica um arquivo de destino (ou seja, um arquivo .dacpac) a ser usado como destino da ação em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de destino será válido. Esse parâmetro será inválido para ações que dão suporte apenas a destinos de banco de dados.|
|**/TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. No Azure AD, recomendamos que esse valor seja maior ou igual a 30 segundos.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se SSL será usado para criptografar a conexão de banco de dados de destino e ignorar a cadeia de certificados para validar a confiança. |
|**/TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de domínio ou a ID do locatário do Azure AD. Essa opção é necessária para dar suporte a usuários convidados ou importados do Azure AD e a contas Microsoft, como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário padrão do Azure AD será usada, supondo que o usuário autenticado seja um usuário nativo desse AD. No entanto, nesse caso, não há suporte para usuários convidados ou importados e/ou contas da Microsoft hospedadas nesse Azure AD, e a operação falhará. <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação universal deve ser usada. Quando definido como True, o protocolo de autenticação interativo é ativado para dar suporte a MFA (autenticação multifator). Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo que exige que o usuário digite seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication está definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/scs). Quando /UniversalAuthentication está definido como False, a autenticação do Azure AD deve ser especificada em SourceConnectionString (/scs). <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e SQL Data Warehouse (suporte SSMS a MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/Variables:**|**/v**|{PropertyName}={Value}|Especifica um par nome-valor para uma variável específica de ação;{NomeDaVariável}={Valor}. O arquivo DACPAC contém a lista de variáveis SQLCMD válidas. Ocorrerá um erro se não for fornecido um valor para cada variável. |

### <a name="properties-specific-to-the-script-action"></a>Propriedades específicas da ação Script

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|Especifica argumentos adicionais de colaborador de implantação para os colaboradores de implantação. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula.
|**/p:**|AdditionalDeploymentContributors=(STRING)|Especifica colaboradores adicionais de implantação que devem ser executados quando o DACPAC é implantado. Ele deve ser em formato de lista delimitada por ponto e vírgula com os IDs ou nomes totalmente qualificados do colaborador de compilação.
|**/p:**|AdditionalDeploymentContributorPaths=(STRING)| Especifica caminhos para carregar colaboradores de implantação adicionais. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula. | 
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|Essa propriedade é usada pela implantação de SqlClr para descartar os assemblies com bloqueio como parte do plano de implantação. Por padrão, os assemblies de bloqueio/referência bloquearão uma atualização de assembly se o assembly de referência precisar ser descartado.
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|Especifica se a ação deve continuar apesar de plataformas do SQL Server potencialmente incompatíveis.
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|Não bloqueie a movimentação de dados em uma tabela que tenha Segurança em Nível de Linha se essa propriedade estiver definida como true. O padrão é false.
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|Faz backups do banco de dados antes de implantar qualquer alteração.
|**/p:**|BlockOnPossibleDataLoss=(BOOLEAN 'True')|Especifica que o episódio de publicação deverá ser terminado se houver uma possibilidade de perda de dados resultante da operação de publicação.
|**/p:**|BlockWhenDriftDetected=(BOOLEAN 'True')|Especifica se deve bloquear a atualização de um banco de dados cujo esquema não mais corresponda seu registro ou não esteja registrado.
|**/p:**|CommandTimeout=(INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|Especifica se a declaração de variáveis SETVAR devem ser comentadas no script de publicação gerado. Você pode optar por fazer isso se planejar especificar os valores na linha de comando ao publicar usando uma ferramenta como SQLCMD.EXE.
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|Essa configuração dita como a ordenação do banco de dados é tratada durante a implantação; por padrão, a ordenação do banco de dados de destino será atualizada se não corresponder à ordenação especificada pela origem. Quando essa opção estiver configurada, a ordenação do banco de dados de destino (ou do servidor) deverá ser usada.|
|**/p:**|CreateNewDatabase=(BOOLEAN)|Especifica se o banco de dados de destino deve ser atualizado ou removido e recriado quando um banco de dados é publicado.
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Define a edição de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| Especifica o tempo limite de bloqueio do banco de dados em segundos ao executar consultas em SQL Server. Use -1 para esperar indefinidamente.|
|**/p:**|DatabaseMaximumSize=(INT32)|Define o tamanho máximo, em GB, de um Banco de Dados SQL do Azure.
|**/p:**|DatabaseServiceObjective=(STRING)|Define o nível de desempenho de um Banco de Dados SQL do Azure, assim como "P0" ou "S1".
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|Se for verdadeiro, o banco de dados será definido como o Modo de Usuário Único antes da implantação.
|**/p:**|DisableAndReenableDdlTriggers=(BOOLEAN 'True')| Especifica se os gatilhos da DDL (linguagem de definição de dados) são desabilitados no início do processo de publicação e reabilitados no final da ação de publicação.|
|**/p:**|DoNotAlterChangeDataCaptureObjects=(BOOLEAN 'True')|Se for verdadeiro, os objetos do Change Data Capture não serão alterados.
|**/p:**|DoNotAlterReplicatedObjects=(BOOLEAN 'True')|Especifica se os objetos que forem replicados são identificados durante a verificação.
|**/p:**|DoNotDropObjectType=(STRING)|Um tipo de objeto que não deve ser descartado quando DropObjectsNotInSource é verdadeiro. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.
|**/p:**|DoNotDropObjectTypes=(STRING)|Uma lista separada por ponto e vírgula de tipos de objeto que não devem ser removidos quando DropObjectsNotInSource é true. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.
|**/p:**|DropConstraintsNotInSource=(BOOLEAN 'True')|Especifica se as restrições que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você em um banco de dados.|
|**/p:**|DropDmlTriggersNotInSource=(BOOLEAN 'True')|Especifica se gatilhos DML que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você em um banco de dados.|
|**/p:**|DropExtendedPropertiesNotInSource=(BOOLEAN 'True')|Especifica se as propriedades estendidas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar em um banco de dados.|
|**/p:**|DropIndexesNotInSource=(BOOLEAN 'True')|Especifica se índices que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você em um banco de dados.|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|Especifica se objetos que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você em um banco de dados. Esse valor tem precedência sobre DropExtendedProperties.|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|Especifica se as permissões que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidas do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|Especifica se os membros de função que não estão definidos no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar atualizações em um banco de dados.|
|**/p:**|DropStatisticsNotInSource=(BOOLEAN 'True')|Especifica se as estatísticas que não existem no arquivo de instantâneo do banco de dados (.dacpac) serão removidas do banco de dados de destino quando você em um banco de dados.|
|**/p:**|ExcludeObjectType=(STRING)|Um tipo de objeto que deve ser ignorado durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.
|**/p:**|ExcludeObjectTypes=(STRING)|Uma lista, delimitada por ponto e vírgula, de tipos de objetos que devem ser ignorados durante a implantação. Os nomes de tipo de objeto válidos são Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers.
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|Automaticamente fornece um valor padrão ao atualizar uma tabela que contém dados com uma coluna que não permite valores nulos.
|**/p:**|IgnoreAnsiNulls=(BOOLEAN 'True')|Especifica se diferenças na configuração ANSI NULLS deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|Especifica se diferenças no Autorizador deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|Especifica se diferenças nas ordenações de coluna deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|Especifica se as diferenças na ordem das colunas da tabela devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|
|**/p:**|IgnoreComments=(BOOLEAN)|Especifica se diferenças nos comentários deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.
|**/p:**|IgnoreCryptographicProviderFilePath=(BOOLEAN 'True')|Especifica se as diferenças no caminho do arquivo para o provedor de criptografia deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um servidor ou banco de dados.|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DDL (linguagem de definição de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|Especifica se diferenças no esquema padrão deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|Especifica se diferenças na ordem de gatilhos DML (linguagem de manipulação de dados) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|Especifica se diferenças no estado habilitado ou desabilitado de gatilhos DML deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|Especifica se diferenças nas propriedades estendidas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFileAndLogFilePath=(BOOLEAN 'True')|Especifica se diferenças nos caminhos para arquivos e arquivos de log deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFilegroupPlacement=(BOOLEAN 'True')|Especifica se diferenças no posicionamento de objetos em FILEGROUPs deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreFileSize=(BOOLEAN 'True')|Especifica se diferenças nos tamanhos de arquivos deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.|
|**/p:**|IgnoreFillFactor=(BOOLEAN 'True')|Especifica se diferenças no fator de preenchimento de armazenamento de índice deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar.|
|**/p:**|IgnoreFullTextCatalogFilePath=(BOOLEAN 'True')|Especifica se diferenças no caminho do arquivo para o texto completo deverão ser ignoradas ou se um aviso deverá ser emitido quando você publicar em um banco de dados.|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|Especifica se diferenças na semente de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar atualizações em um banco de dados.|
|**/p:**|IgnoreIncrement=(BOOLEAN)|Especifica se diferenças no incremento de uma coluna de identidade deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|Especifica se diferenças nas opções de índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreIndexPadding=(BOOLEAN 'True')|Especifica se diferenças nas opções de preenchimento do índice deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreKeywordCasing=(BOOLEAN 'True')|Especifica se diferenças no uso de maiúsculas e minúsculas em palavras-chave deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|Especifica se diferenças no uso de dicas de bloqueio em índices deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreLoginSids=(BOOLEAN 'True')| Especifica se diferenças no número SID (identificação de segurança) deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|Especifica se as configurações que não sejam para replicação deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme=(BOOLEAN 'True')|Especifica se o posicionamento de um objeto em um esquema de partição deverá ser ignorado ou atualizado quando você publicar em um banco de dados.|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|Especifica se diferenças em esquemas de partição e funções deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnorePermissions=(BOOLEAN)|Especifica se diferenças nas permissões deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreQuotedIdentifiers=(BOOLEAN 'True')|Especifica se diferenças na configuração de identificadores entre aspas deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|Especifica se as diferenças nas associações de logons à função devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|
|**/p:**|IgnoreRouteLifetime=(BOOLEAN 'True')|Especifica se diferenças na quantidade de tempo que o SQL Server retém a rota na tabela de roteamento deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreSemicolonBetweenStatements=(BOOLEAN 'True')|Especifica se diferenças nos pontos e vírgulas entre instruções T-SQL serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|Especifica se diferenças nas opções de tabela serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreTablePartitionOptions=(BOOLEAN)|Especifica se diferenças nas opções de partição de tabela serão ignoradas ou atualizadas quando você publicar em um banco de dados.  Essa opção se aplica somente ao banco de dados de data warehouse do Azure Synapse Analytics.|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|Especifica se diferenças nos objetos de configurações do usuário serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreWhitespace=(BOOLEAN 'True')|Especifica se diferenças de espaço em branco serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para restrições de verificação serão ignoradas ou atualizadas quando você publicar.|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|Especifica se diferenças no valor da cláusula WITH NOCHECK para chaves estrangeiras serão ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|Inclua todos os elementos compostos como parte de uma única operação de publicação.|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|Especifica se instruções transacionais deverão ser usadas quando possível quando você publicar em um banco de dados.|
|**/p:**|LongRunningCommandTimeout=(INT32)| Especifica o tempo limite do comando de execução prolongada em segundos ao executar consultas com relação ao SQL Server. Use 0 para esperar indefinidamente.|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|Especifica se a publicação sempre deverá cancelar e recriar um assembly se houver uma diferença em vez de emitir uma instrução ALTER ASSEMBLY.|
|**/p:**|PopulateFilesOnFileGroups=(BOOLEAN 'True')|Especifica se um novo arquivo também será criado quando um novo FileGroup for criado no banco de dados de destino.|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|Especifica se o esquema está registrado com o servidor de banco de dados.|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|Especifica se os colaboradores de DeploymentPlanExecutor devem ser executados quando outras operações forem executadas.|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|Especifica se diferenças na ordenação do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|Especifica se diferenças na compatibilidade do banco de dados deverão ser ignoradas ou atualizadas quando você publicar em um banco de dados.|
|**/p:**|ScriptDatabaseOptions=(BOOLEAN 'True')|Especifica se as propriedades do banco de dados de destino devem ser definidas ou atualizadas como parte da ação de publicação.|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|Especifica se as instruções são geradas no script de publicação para verificar se o nome do banco de dados e o nome do servidor correspondem aos nomes especificados no projeto de banco de dados.|
|**/p:**|ScriptFileSize=(BOOLEAN)|Controla se o tamanho é especificado ao adicionar um arquivo a um grupo de arquivos.|
|**/p:**|ScriptNewConstraintValidation=(BOOLEAN 'True')|No final da publicação, todas as restrições serão verificadas em conjunto, evitando erros de dados causados por uma verificação ou restrição de chave estrangeira no meio da publicação. Se definido como False, as restrições serão publicadas sem verificar os dados correspondentes.|
|**/p:**|ScriptRefreshModule=(BOOLEAN 'True')|Inclua instruções de atualização no fim do script de publicação.|
|**/p:**|Storage=({File&#124;Memory})|Especifica como os elementos são armazenados ao criar o modelo de banco de dados. Por razões de desempenho, o padrão é InMemory. Para bancos de dados grandes, é necessário realizar armazenamento de backup de arquivos.|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|Especifica se os erros encontrados durante a verificação de publicação devem ser tratados como avisos. A verificação é executada em relação ao plano de implantação gerado antes de o plano ser executado em relação ao banco de dados de destino. A verificação do plano detecta problemas, como a perda de objetos apenas de destino (por exemplo, índices), que devem ser cancelados para fazer uma alteração. A verificação também detectará situações em que existem dependências (como tabelas ou exibições) devido a uma referência a um projeto composto, mas não existem no banco de dados de destino. Você pode optar por fazer isso para obter uma lista completa de todos os problemas, em vez de interromper a ação de publicação no primeiro erro.|
|**/p:**|UnmodifiableObjectWarnings=(BOOLEAN 'True')|Especifica se devem ser gerados avisos quando diferenças forem localizadas em objetos que não podem ser modificados, por exemplo, se o tamanho ou os caminhos de arquivo forem diferentes para um arquivo.|
|**/p:**|VerifyCollationCompatibility=(BOOLEAN 'True')|Especifica se a compatibilidade de ordenação é verificada.
|**/p:**|VerifyDeployment=(BOOLEAN 'True')|Especifica se devem ser executadas verificações antes da publicação, o que interromperá a ação de publicação se houver problemas que possam bloquear uma publicação bem-sucedida. Por exemplo, sua ação de publicação poderá ser interrompida se você tiver chaves estrangeiras no banco de dados de destino que não existem no projeto de banco de dados, o que causará erros ao publicar.|

## <a name="exit-codes"></a>Códigos de saída

Comandos que retornam os seguintes códigos de saída:

- 0 = êxito
- diferente de zero = falha
