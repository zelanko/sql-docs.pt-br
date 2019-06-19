---
title: Usar MSDeploy com o provedor do dbSqlPackage | Microsoft Docs
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 213b91ab-03e9-431a-80f0-17eed8335abe
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6e58a1f5e36ea4c8f9412c06ad08729716d02eef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65101965"
---
# <a name="using-msdeploy-with-dbsqlpackage-provider"></a>Usando MSDeploy com o provedor do dbSqlPackage
O **DbSqlPackage** é um provedor do **MSDeploy** que permite interagir com bancos de dados do SQL Server/SQL Azure. O **DbSqlPackage** dá suporte às seguintes ações:  
  
-   **Extrair**: cria um arquivo de instantâneo de banco de dados (.dacpac) de bancos de dados do SQL Server ou do SQL Azure.  
  
-   **Publicar**: atualiza um esquema de banco de dados incrementalmente para que corresponda ao esquema de um arquivo .dacpac de origem.  
  
-   **DeployReport**: cria um relatório XML das alterações que teriam sido feitas por uma ação de publicação.  
  
-   **Script**: cria um script Transact\-SQL equivalente ao script executado pela ação Publish.  
  
Para saber mais sobre DACFx, consulte a documentação da API gerenciada DACFx [https://msdn.microsoft.com/library/microsoft.sqlserver.dac.aspx](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.aspx) ou [SqlPackage.exe](../tools/sqlpackage.md) (ferramenta de linha de comando do DACFx).  
  
> [!IMPORTANT]  
> O recurso de provedor dbSqlPackage será removido na próxima versão principal do Visual Studio. Para obter informações sobre como fazer a publicação do banco de dados com a Implantação da Web, consulte o [provedor dbDacFx para obter a publicação de banco de dados Incremental](https://www.iis.net/learn/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing).  
  
## <a name="command-line-syntax"></a>Sintaxe da linha de comando  
**MSDeploy** com o provedor **dbSqlPackage** usa uma linha de comando do seguinte formato:  
  
```  
  
MSDeploy -verb: MSDeploy-verb -source:dbSqlPackage="Input"[,dbSqlPackage-source-parameters] -dest:dpSqlPackage="Input"[,dbSqlPackage-target-parameters]  
```  
  
## <a name="ms-deploy-verbs"></a>Verbos do MS-Deploy  
Você especifica verbos do MS-Deploy usando a opção **-verb** na linha de comando do MS-Deploy. O provedor **dbSqlPackage** dá suporte aos seguintes verbos **MSDeploy**:  
  
|Verbo|Descrição|  
|--------|---------------|  
|dump|Fornece informações, que incluem o nome, o número da versão e a descrição, sobre um banco de dados de origem contido em um arquivo .dacpac. Especifique o banco de dados de origem usando o seguinte formato na linha de comando:<br /><br />**msdeploy -verb:dump -source:dbSqlPackage="** _.dacpac-file-path_ **"**|  
|sync|Especifica as ações do dbSqlPackage usando o seguinte formato na linha de comando:<br /><br />**msdeploy -verb:sync -source:dbSqlPackage**="input" _[,DbSqlPackage-source-parameters] -_ **dest:dbSqlPackage**="input" *[,DbSqlPackage-destination-parameters]*<br /><br />Consulte as seções abaixo para obter os parâmetros válidos de origem e destino para o verbo de sincronização.|  
  
## <a name="dbsqlpackage-source"></a>Origem do dbSqlPackage  
O provedor **dbSqlPackage** usa uma entrada que é uma cadeia de conexão válida do SQL Server/SQL Azure ou um caminho para um arquivo .dacpac no disco.  A sintaxe para especificar a fonte de entrada para o provedor é a seguinte:  
  
|Entrada|Padrão|Descrição|  
|---------|-----------|---------------|  
|**-source:dbSqlPackage=** {*input*}|**N/A**|*input* é uma cadeia de conexão válida do SQL Server ou do SQL Azure ou um caminho para um arquivo .dacpac no disco.<br /><br />**OBSERVAÇÃO:** as únicas propriedades de cadeia de conexão com suporte ao usar uma cadeia de conexão como fonte de entrada são *InitialCatalog, DataSource, UserID, Password, IntegratedSecurity, Encrypt, TrustServerCertificate* e *ConnectionTimeout*.|  
  
Se sua fonte de entrada for uma cadeia de conexão para um banco de dados SQL Server/SQL Azure ativo, o **dbSqlPackage** extrairá um instantâneo de banco de dados (na forma de um arquivo .dacpac) em um banco de dados SQL Server/SQL Azure ativo.  
  
Os parâmetros de **Origem** são:  
  
|Parâmetro|Padrão|Descrição|  
|-------------|-----------|---------------|  
|**Perfil**:{ *string*}|N/A|Especifica o caminho de um arquivo para um perfil de publicação do DAC. O perfil define uma coleção de propriedades e variáveis para serem usadas ao gerar o dacpac resultante. O perfil de publicação é passado para o destino e usado como as opções padrão ao realizar uma ação **Publish**, **Script** ou **DeployReport**.|  
|**DacApplicationName**={ *string* }|Nome do banco de dados|Define o nome do aplicativo a ser armazenado nos metadados do DACPAC. A cadeia de caracteres padrão é o nome do banco de dados.|  
|**DacMajorVersion** ={*integer*}|**1**|Define a versão principal a ser armazenada nos metadados do DACPAC.|  
|**DacMinorVersion**={*integer*}|**0**|Define a versão secundária a ser armazenada nos metadados do DACPAC.|  
|**DacApplicationDescription**={ *string* }|N/A|Define a descrição do aplicativo a ser armazenada nos metadados do DACPAC.|  
|**ExtractApplicationScopedObjectsOnly = {True &#124; False}**|**Verdadeiro**|Se for **True**, extrairá apenas objetos com escopo do aplicativo da origem. Se for **False**, extrairá os objetos com escopo de aplicativo e os objetos sem escopo de aplicativo.|  
|**ExtractReferencedServerScopedElements={True &#124; False}**|**Verdadeiro**|Se **True**, extrairá logon, auditoria de servidor e objetos de credencial referenciados pelos objetos do banco de dados de origem.|  
|**ExtractIgnorePermissions={True &#124; False}**|**Falso**|Se for **True**, ignorará permissões de extração para todos os objetos extraídos. Se for **False**, não extrairá.|  
|**ExtractStorage={File&#124;Memory}**|**File**|Especifica o tipo de armazenamento de backup para o modelo de esquema usado durante a extração.|  
|**ExtractIgnoreExtendedProperties={True&#124;False}**|**Falso**|Especifica se as propriedades estendidas devem ser ignoradas.|  
|**VerifyExtraction = {True&#124;False}**|**Falso**|Especifica se o dacpac extraído deve ser verificado.|  
  
## <a name="dbsqlpackage-destination"></a>Destino do DbSqlPackage  
O provedor do **dbSqlPackage** aceita uma cadeia de conexão válida do SQL Server/SQL Azure ou um caminho para um arquivo .dacpac no disco como a entrada de destino.  A sintaxe para especificar o destino para o provedor é a seguinte:  
  
|Entrada|Padrão|Descrição|  
|---------|-----------|---------------|  
|-**dest:dbSqlPackage**={*input*}|N/A|*input* é uma cadeia de conexão válida do SQL Server ou do SQL Azure ou um caminho completo ou parcial para um arquivo .dacpac no disco. Se *input* for um caminho de arquivo, nenhum outro parâmetro poderá ser especificado.|  
  
Os parâmetros de **Destino** a seguir estão disponíveis para todas as operações **dbSqlPackage**:  
  
|Propriedade|Padrão|Descrição|  
|------------|-----------|---------------|  
|**Action={Publish&#124;DeployReport&#124;Script}**|N/A|Os parâmetros opcionais que especificam a ação a ser realizada no **Destino**.|  
|**AllowDropBlockingAssemblies ={True &#124; False}**|**Falso**|Especifica se a publicação do **SqlClr** cancela assemblies de bloqueio como parte do plano de implantação. Por padrão, os assemblies de bloqueio ou de referência bloquearão uma atualização de assembly se o assembly de referência precisar ser cancelado.|  
|**AllowIncompatiblePlatform={True &#124; False}**|**Falso**|Especifica se a ação de publicação deve avançar apesar de plataformas do SQL Server potencialmente incompatíveis.|  
|**BackupDatabaseBeforeChanges={True &#124; False}**|**Falso**|Faz backups do banco de dados antes de implantar qualquer alteração.|  
|**BlockOnPossibleDataLoss={ True &#124; False}**|**Verdadeiro**|Especifica se o episódio de publicação será terminado se a operação de publicação puder provocar perda de dados.|  
|**BlockWhenDriftDetected={ True &#124; False}**|**Verdadeiro**|Especifica se deve bloquear a atualização de um banco de dados cujo esquema não mais corresponda seu registro ou não esteja registrado.|  
|**CommentOutSetVarDeclarations= {True &#124; False}**|**Falso**|Especifica se as declarações da variável **SETVAR** são comentadas no script de publicação gerado. Você pode optar por fazer isso se planejar usar uma ferramenta como **SQLCMD.EXE** para especificar os valores na linha de comando ao publicar.|  
|**CompareUsingTargetCollation={ True &#124; False}**|**Falso**|Essa configuração dita como a ordenação do banco de dados é tratada durante a implantação; por padrão, a ordenação do banco de dados de destino será atualizada se não corresponder à ordenação especificada pela origem.  Quando essa opção estiver configurada, a ordenação do banco de dados de destino (ou do servidor) deverá ser usada.|  
|**CreateNewDatabase={ True &#124; False}**|**Falso**|Especifica se o banco de dados de destino deve ser atualizado ou removido e recriado quando um banco de dados é publicado.|  
|**DeployDatabaseInSingleUserMode={ True &#124; False}**|**Falso**|Se for **True**, o banco de dados será definido como o Modo de Usuário Único antes da implantação.|  
|**DisableAndReenableDdlTriggers={True &#124; False}**|**Verdadeiro**|Especifica se os gatilhos da DDL (linguagem de definição de dados) são desabilitados no início do processo de publicação e reabilitados no final da ação de publicação.|  
|**DoNotAlterChangeDataCaptureObjects={ True &#124; False}**|**Verdadeiro**|Se for **True**, os objetos da captura de dados de alterações não serão alterados.|  
|**DoNotAlterReplicatedObjects=( True &#124; False}**|**Verdadeiro**|Especifica se os objetos que forem replicados são identificados durante a verificação.|  
|**DropConstraintsNotInSource= {True &#124; False}**|**Verdadeiro**|Especifica se a ação de publicação cancela restrições não existentes no instantâneo de banco de dados (.dacpac) do banco de dados de destino quando você publica em um banco de dados.|  
|**DropDmlTriggersNotInSource= {True &#124; False}**|**Verdadeiro**|Especifica se a ação de publicação cancela gatilhos DML (linguagem de manipulação de dados) não existentes no instantâneo de banco de dados (.dacpac) do banco de dados de destino quando você publica em um banco de dados.|  
|**DropExtendedPropertiesNotInSource= {True &#124; False}**|**Verdadeiro**|Especifica se a ação de publicação cancela propriedades estendidas não existentes no instantâneo de banco de dados (.dacpac) do banco de dados de destino quando você publica em um banco de dados.|  
|**DropIndexesNotInSource= {True &#124; False}**|**Verdadeiro**|Especifica se a ação de publicação cancela índices não existentes no instantâneo de banco de dados (.dacpac) do banco de dados de destino quando você publica em um banco de dados.|  
|**DropObjectsNotInSource= {True &#124; False}**|**Falso**|Especifica se os objetos que não existem no arquivo do instantâneo de banco de dados (.dacpac) serão removidos do banco de dados de destino quando você publicar em um banco de dados.|  
|**DropPermissionsNotInSource= {True &#124; False}**|**Falso**|Especifica se a ação de publicação cancela permissões não existentes no instantâneo de banco de dados (.dacpac) do banco de dados de destino quando você publica em um banco de dados.|  
|**DropRoleMembersNotInSource= {True &#124; False}**|**Falso**|Especifica se a ação de publicação cancela membros de função não existentes no instantâneo de banco de dados (.dacpac) do banco de dados de destino quando você publica em um banco de dados.|  
|**GenerateSmartDefaults={True &#124; False}**|**Falso**|Especifica se o **SqlPackage.exe** fornece automaticamente um valor padrão quando atualiza uma tabela que contém dados com uma coluna que não permite valores nulos.|  
|**IgnoreAnsiNulls= {True &#124; False}**|**Falso**|Especifica se as diferenças na configuração do **ANSI NULLS** devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreAuthorizer= {True &#124; False}**|**Falso**|Especifica se as diferenças no Autorizador devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreColumnCollation= {True &#124; False}**|**Falso**|Especifica se as diferenças na ordenação de colunas devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreComments= {True &#124; False}**|**Falso**|Especifica se as diferenças na ordem de comentários devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreCryptographicProviderFile= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças no caminho do arquivo de um provedor criptográfico devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreDdlTriggerOrder= {True &#124; False}**|**Falso**|Especifica se as diferenças na ordem de gatilhos DDL (linguagem de definição de dados) devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreDdlTriggerState={True &#124; False}**|**Falso**|Especifica se as diferenças no estado habilitado ou desabilitado de gatilhos DDL devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreDefaultSchema={True &#124; False}**|**Falso**|Especifica se as diferenças no esquema padrão devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreDmlTriggerOrder= {True &#124; False}**|**Falso**|Especifica se as diferenças na ordem de gatilhos DML devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreDmlTriggerState= {True &#124; False}**|**Falso**|Especifica se as diferenças no estado habilitado ou desabilitado de gatilhos DML devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreExtendedProperties= {True &#124; False}**|**Falso**|Especifica se as diferenças nas propriedades estendidas devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreFileAndLogFilePath={True &#124; False}**|**Verdadeiro**|Especifica se as diferenças nos caminhos de arquivos e arquivos de log devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreFilegroupPlacement= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças no posicionamento dos **FILEGROUPS** devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreFileSize= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças nos tamanhos dos arquivos devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreFillFactor= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças nos fatores de preenchimento devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
  
|Propriedade|Padrão|Descrição|  
|------------|-----------|---------------|  
|**IgnoreFullTextCatalogFilePath= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças no caminho para arquivos de índice de texto completo devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreIdentitySeed= {True &#124; False}**|**Falso**|Especifica se as diferenças na semente de uma coluna de identidade devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreIncrement= {True &#124; False}**|**Falso**|Especifica se as diferenças no incremento de uma coluna de identidade devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreIndexOptions ={True &#124; False}**|**Falso**|Especifica se as diferenças nas opções de índice devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreIndexPadding= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças no preenchimento de índice devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreKeywordCasing= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças em maiúsculas e minúsculas de palavra-chave devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreLockHintsOnIndexes= {True &#124; False}**|**Falso**|Especifica se as diferenças nas dicas de bloqueio em índices devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreLoginSids= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças no SID (identificador de segurança) devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreNotForReplication= {True &#124; False}**|**Falso**|Especifica se as diferenças na configuração de não replicação devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreObjectPlacementOnPartitionScheme= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças no posicionamento de um objeto em um esquema de partição devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnorePartitionSchemes= {True &#124; False}**|**Falso**|Especifica se as diferenças nos esquemas e funções de partição devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnorePermissions= {True &#124; False}**|**Falso**|Especifica se as diferenças nas permissões devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreQuotedIdentifiers= {True &#124; False}**|**Falso**|Especifica se as diferenças nas configurações do identificador entre aspas devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreRoleMembership={True &#124; False}**|**Falso**|Especifica se as diferenças nas associações de logons à função devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreRouteLifetime= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças nas associações de função de logons devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreSemicolonBetweenState= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças em pontos-e-vírgulas entre instruções Transact-SQL devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreTableOptions= {True &#124; False}**|**Falso**|Especifica se as diferenças nas opções de tabela devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreUserSettingsObjects= {True &#124; False}**|**Falso**|Especifica se as diferenças nas opções de configuração do usuário devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreWhitespace= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças no espaço em branco devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreWithNocheckOnCheckConstraints={True &#124; False}**|**Falso**|Especifica se as diferenças no valor da cláusula **WITH NOCHECK** para restrições de verificação devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IgnoreWithNocheckOnForeignKeys={True &#124; False}**|**Falso**|Especifica se as diferenças no valor da cláusula **WITH NOCHECK** para chaves estrangeiras devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**IncludeCompositeObjects= {True &#124; False}**|**Falso**|Especifica se todos os elementos compostos devem ser incluídos como parte de uma única operação de publicação.|  
|**IncludeTransactionalScripts={True &#124; False}**|**Falso**|Especifica se as instruções transacionais devem ser usadas sempre que possível quando você publica em um banco de dados.|  
|**NoAlterStatementsToChangeClrTypes={True &#124; False}**|**Falso**|Especifica se a publicação sempre deverá cancelar e recriar um assembly se houver uma diferença em vez de emitir uma instrução ALTER ASSEMBLY.|  
|**PopulateFilesOnFilegroups= {True &#124; False}**|**Verdadeiro**|Especifica se um novo arquivo também é criado quando você cria um novo **FileGroup** no banco de dados de destino.|  
|**RegisterDataTierApplication={True &#124; False}**|**Falso**|Especifica se o esquema está registrado com o servidor de banco de dados.|  
|**ScriptDatabaseCollation {True &#124; False}**|**Falso**|Especifica se as diferenças na ordenação de banco de dados devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**ScriptDatabaseCompatibility= {True &#124; False}**|**Verdadeiro**|Especifica se as diferenças na compatibilidade de banco de dados devem ser ignoradas ou atualizadas quando você publica em um banco de dados.|  
|**ScriptDatabaseOptions= {True &#124; False}**|**Verdadeiro**|Especifica se as propriedades do banco de dados de destino devem ser definidas ou atualizadas quando você publica em um banco de dados.|  
|**ScriptFileSize={True &#124; False}**|**Falso**|Controla se o tamanho é especificado ao adicionar um arquivo a um grupo de arquivos.|  
|**ScriptNewConstraintValidation= {True &#124; False}**|**Verdadeiro**|Especifica se todas as restrições devem ser verificadas como um conjunto no final da publicação, evitando erros de dados provocados por uma restrição de verificação ou de chave estrangeira no meio da ação de publicação. Se essa opção for **False**, as restrições serão publicadas sem verificar os dados correspondentes.|  
|**ScriptDeployStateChecks={True &#124; False}**|**Falso**|Especifica se as instruções devem ser geradas no script de publicação para verificar se os nomes de banco de dados e de servidor correspondem aos nomes especificados no projeto de banco de dados.|  
|**ScriptRefreshModule= {True &#124; False}**|**Verdadeiro**|Especifica se as instruções de atualização devem ser incluídas no final do script de publicação.|  
|**Storage={File&#124;Memory}**|**Memória**|Especifica como os elementos são armazenados ao criar o modelo de banco de dados. Por razões de desempenho, o padrão é **Memória**. Para bancos de dados muito grandes, é necessário realizar armazenamento de backup de arquivos.|  
|**TreatVerificationErrorsAsWarnings= {True &#124; False}**|**Falso**|Especifica se os erros que ocorrem durante a verificação de publicação como avisos devem ser tratados. A verificação é executada em relação ao plano de implantação gerado antes de o plano ser executado em relação ao banco de dados de destino. A verificação do plano detecta problemas, como a perda de objetos apenas de destino (por exemplo, índices), que devem ser cancelados para fazer uma alteração. A verificação também detecta situações onde existem dependências (como tabelas ou exibições) devido a uma referência a um projeto composto, mas não existem no banco de dados de destino. Você pode optar por tratar erros de verificação como avisos para obter uma lista completa de problemas, em vez de permitir que a ação de publicação seja interrompida quando ocorre o primeiro erro.|  
|**UnmodifiableObjectWarnings= {True &#124; False}**|**Verdadeiro**|Especifica se devem ser gerados avisos quando diferenças forem localizadas em objetos que não podem ser modificados (por exemplo, se o tamanho ou os caminhos de arquivo forem diferentes para um arquivo).|  
|**VerifyCollationCompatibility={True &#124; False}**|**Verdadeiro**|Especifica se a compatibilidade de ordenação é verificada.|  
|**VerifyDeployment={True &#124; False}**|**Verdadeiro**|Especifica se devem ser executadas verificações antes da publicação, que interromperão a ação de publicação se estiverem presentes problemas que possam bloquear uma publicação bem-sucedida. Por exemplo, sua ação de publicação poderá ser interrompida se você obtiver erros durante a publicação porque chaves estrangeiras no banco de dados de destino não existem no projeto de banco de dados.|  
  
> [!NOTE]  
> Os parâmetros de destino especificados serão sobrescritos pelos especificados no perfil Publish de origem.  
  
> [!NOTE]  
> As variáveis e os valores do **SQLCMD** devem ser especificados no parâmetro de origem do perfil de publicação, porque não podem ser especificados como um parâmetro de destino.  
  
Os parâmetros de **Destino** a seguir estão disponíveis para todas as operações **DeployReport** e **Script**:  
  
|Parâmetro|Padrão|Descrição|  
|-------------|-----------|---------------|  
|**OutputPath**={ *string* }|N/A|Parâmetro opcional que instrui o **dbSqlPackage** para criar o arquivo de saída XML do DeployReport ou arquivo de saída de SQL do Script no local do disco especificado por *cadeia de caracteres*. Essa ação substitui todos os scripts que residem atualmente no local fornecido por cadeia de caracteres.|  
  
> [!NOTE]  
> Se o parâmetro **OutputPath** não for fornecido para uma ação **DeployReport** ou **Script**, a saída será retornada como uma mensagem.  
  
## <a name="examples"></a>Exemplos  
Veja a seguir uma sintaxe de exemplo para uma operação **Extract** usando **dbSqlPackage**:  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source connection string>",<source parameter> -dest:dbSqlPackage="<target dacpac file path>"  
```  
  
Veja a seguir uma sintaxe de exemplo para uma operação **Publish** usando **dbSqlPackage**:  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source dacpac file path>" -dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=Publish,<destination parameters>  
```  
  
Veja a seguir uma sintaxe de exemplo para uma operação **DeployReport** usando **dbSqlPackage**:  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source dacpac file path>" -dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=DeployReport,OutputPath="<path to output XML file>",<destination parameters>  
```  
  
Veja a seguir uma sintaxe de exemplo para uma operação **Script** usando **dbSqlPackage**:  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source dacpac file path>" -dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=Script,OutputPath="<path to output sql script>",<destination parameters>  
```  
  
