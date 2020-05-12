---
title: DATABASEPROPERTYEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATABASEPROPERTYEX
- DATABASEPROPERTYEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DATABASEPROPERTYEX function
- displaying database properties
- database properties [SQL Server]
ms.assetid: 8a9e0ffb-28b5-4640-95b2-a54e3e5ad941
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f0bae370acd535f331d287cea38de04375891db0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823882"
---
# <a name="databasepropertyex-transact-sql"></a>DATABASEPROPERTYEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Para um banco de dados especificado em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa função retorna a configuração atual da opção ou propriedade de banco de dados especificada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATABASEPROPERTYEX ( database , property )  
```  
  
## <a name="arguments"></a>Argumentos  
*database*  
É uma expressão que especifica o nome do banco de dados para o qual `DATABASEPROPERTYEX` retorna as informações da propriedade nomeada. *database* tem um tipo de dados **nvarchar (128)** .  

Para [!INCLUDE[ssSDS](../../includes/sssds-md.md)], `DATABASEPROPERTYEX` requer o nome do banco de dados atual. Retornará NULL para todas as propriedades se for fornecido um nome de banco de dados diferente.
  
*property*  
É uma expressão que especifica o nome da propriedade do banco de dados a ser retornada. *property* tem um tipo de dados **varchar (128)** e dá suporte a um dos valores nesta tabela:
  
> [!NOTE]  
>  Se o banco de dados ainda não foi iniciado, chamadas para `DATABASEPROPERTYEX` retornarão NULL se `DATABASEPROPERTYEX` recuperar esses valores por acesso direto de banco de dados, em vez de recuperação de metadados. Um banco de dados com AUTO_CLOSE definida como ON ou, caso contrário, offline, é definido como "não iniciado".  
  
|Propriedade|Descrição|Valor retornado|  
|---|---|---|
|Collation|O nome da ordenação padrão para o banco de dados.|Nome da ordenação<br /><br /> NULL: O banco de dados não foi iniciado.<br /><br /> Tipo de dados base: **nvarchar(128)**|  
|ComparisonStyle|O estilo de comparação da ordenação do Windows. Use os seguintes valores de estilo para criar um bitmap para o valor ComparisonStyle concluído:<br /><br /> Ignorar maiúsculas e minúsculas: 1<br /><br /> Ignorar acento: 2<br /><br /> Ignorar Kana: 65536<br /><br /> Ignorar largura: 131072<br /><br /> <br /><br /> Por exemplo, o padrão de 196609 é o resultado de combinar as opções Ignorar maiúsculas e minúsculas, Ignorar Kana e Ignorar largura.|Retorna o estilo de comparação.<br /><br /> Retorna 0 para todas as ordenações primárias.<br /><br /> Tipo de dados base: **int**|  
|Edition|A camada de edição ou de serviço do banco de dados.|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].<br /><br /> <br /><br /> Uso Geral<br /><br /> Comercialmente Crítico<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium<br /><br /> Sistema (para o banco de dados mestre)<br /><br /> NULL: O banco de dados não foi iniciado.<br /><br /> Tipo de dados base: **nvarchar**(64)|  
|IsAnsiNullDefault|O banco de dados segue regras de ISO por permitir valores nulos.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsAnsiNullsEnabled|Todas as comparações com um nulo são avaliadas como desconhecido.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsAnsiPaddingEnabled|As cadeias de caracteres são convertidas na mesma largura antes da comparação ou inserção.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsAnsiWarningsEnabled|Mensagens de erro ou de aviso do SQL Server quando ocorrem condições de erro padrão.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsArithmeticAbortEnabled|Consultas são encerradas quando um erro de estouro ou divisão por zero ocorre durante a execução da consulta.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsAutoClose|O banco de dados é desligado corretamente e libera recursos depois da saída do último usuário.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsAutoCreateStatistics|O otimizador de consulta cria estatísticas de coluna única, conforme necessário, para melhorar o desempenho de consulta.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsAutoCreateStatisticsIncremental|As estatísticas e coluna única criadas automaticamente são incrementais quando possível.|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsAutoShrink|Os arquivos de banco de dados são candidatos à redução automática periódica.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsAutoUpdateStatistics|Quando uma consulta usa estatísticas existentes potencialmente desatualizadas, o otimizador de consulta atualiza as estatísticas.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada não válida<br /><br /> Tipo de dados base: **int**|
|IsClone|O banco de dados é uma cópia somente de esquema e estatísticas de um banco de dados de usuário criado com DBCC CLONEDATABASE. Confira o [artigo do Suporte da Microsoft](https://support.microsoft.com/help/3177838) para obter mais informações.|**Aplica-se ao**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e posterior.<br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**| 
|IsCloseCursorsOnCommitEnabled|Quando uma transação é confirmada, todos os cursores abertos serão fechados.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsFulltextEnabled|O banco de dados está habilitado para indexação de texto completo e semântica.|**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br /><br /> <br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada não válida<br /><br /> Tipo de dados base: **int**<br /><br /> **Observação:** O valor dessa propriedade agora não tem nenhum efeito. Os bancos de dados de usuário são sempre habilitados para pesquisa de texto completo. Uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] removerá essa propriedade. Não use essa propriedade em desenvolvimentos novos e modifique, assim que possível, os aplicativos que atualmente a usam.|  
|IsInStandBy|O banco de dados está online como somente leitura, com o log de restauração permitido.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsLocalCursorsDefault|As declarações de cursor assumem LOCAL como padrão.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsMemoryOptimizedElevateToSnapshotEnabled|As tabelas com otimização de memória são acessadas usando o isolamento SNAPSHOT quando a configuração de sessão TRANSACTION ISOLATION LEVEL é definida como READ COMMITTED, READ UNCOMMITTED ou um nível de isolamento inferior.|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> <br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> Tipo de dados base: **int**|  
|IsMergePublished|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à publicação da tabela de um banco de dados para replicação de mesclagem, caso a replicação tenha sido instalada.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsNullConcat|O operando de concatenação nulo resulta em NULL.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsNumericRoundAbortEnabled|Erros são gerados quando a perda de precisão ocorre em expressões.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsParameterizationForced|A opção SET de banco de dados PARAMETERIZATION é FORCED.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida|  
|IsQuotedIdentifiersEnabled|São permitidas aspas duplas em identificadores.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsPublished|Se a replicação tiver sido instalada, haverá suporte de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à publicação de tabelas do banco de dados por instantâneo ou replicação transacional.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsRecursiveTriggersEnabled|O acionamento recursivo dos disparadores está habilitado.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsSubscribed|O banco de dados é assinado para uma publicação.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsSyncWithBackup|Este é um banco de dados publicado ou um banco de dados de distribuição e dá suporte à restauração sem romper a replicação transacional.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**|  
|IsTornPageDetectionEnabled|O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] detecta operações de E/S incompletas causadas por falhas de energia ou outros problemas no sistema.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**| 
|IsVerifiedClone|O banco de dados é uma cópia somente de esquema e estatísticas de um banco de dados de usuário criado usando a opção WITH VERIFY_CLONEDB de DBCC CLONEDATABASE. Confira este [artigo do Suporte da Microsoft](https://support.microsoft.com/help/3177838) para obter mais informações.|**Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2.<br /><br /> <br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **int**| 
|IsXTPSupported|Indica se o banco de dados dá suporte a OLTP in-memory, ou seja, criação e uso de tabelas com otimização de memória e módulos compilados nativamente.<br /><br /> Específico ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> IsXTPSupported não depende da existência de um grupo de arquivos MEMORY_OPTIMIZED_DATA, que é necessário para a criação de objetos OLTP in-memory.|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: Entrada inválida, um erro ou não aplicável<br /><br /> Tipo de dados base: **int**|  
|LastGoodCheckDbTime|A data e hora do último DBCC CHECKDB bem-sucedido executado no banco de dados especificado.<sup>1</sup> Se DBCC CHECKDB não tiver sido executado em um banco de dados, 1900-01-01 00:00:00.000 será retornado.|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] do SP2 em diante.</br>[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] a partir da CU9.</br>[!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] ou posterior.</br>Banco de Dados SQL do Azure.<br/><br/>Um valor datetime<br /><br /> NULL: Entrada inválida<br /><br /> Tipo de dados base: **datetime**| 
|LCID|O LCID (identificador de localidade) do Windows da ordenação.|Valor LCID (em formato decimal).<br /><br /> Tipo de dados base: **int**|  
|MaxSizeInBytes|Tamanho máximo do banco de dados, em bytes.|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].<br /><br /> <br /><br /> 1073741824<br /><br /> 5368709120<br /><br /> 10737418240<br /><br /> 21474836480<br /><br /> 32212254720<br /><br /> 42949672960<br /><br /> 53687091200<br /><br /> NULL: O banco de dados não foi iniciado<br /><br /> Tipo de dados base: **bigint**|  
|Recuperação|Modelo de recuperação de banco de dados|FULL: Modelo de recuperação completa<br /><br /> BULK_LOGGED: Modelo registrado em log em massa<br /><br /> SIMPLE: Modelo de recuperação simples<br /><br /> Tipo de dados base: **nvarchar(128)**|  
|ServiceObjective|Descreve o nível de desempenho do banco de dados no [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ou [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|Um dos seguintes:<br /><br /> Nulo: banco de dados não iniciado<br /><br /> Compartilhado (para edições Web/Business)<br /><br /> Basic<br /><br /> S0<br /><br /> S1<br /><br /> S2<br /><br /> S3<br /><br /> P1<br /><br /> P2<br /><br /> P3<br /><br /> ElasticPool<br /><br /> Sistema (para o banco de dados mestre)<br /><br /> Tipo de dados base: **nvarchar(32)**|  
|ServiceObjectiveId|O id do objetivo de serviço em [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|**uniqueidentifier** que identifica o objetivo de serviço.|  
|SQLSortOrder|Identificação de ordem de classificação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com suporte em versões anteriores do SQL Server.|0: o banco de dados usa ordenação do Windows<br /><br /> >0: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID da ordem de classificação<br /><br /> NULL: entrada inválida ou banco de dados não foi iniciado<br /><br /> Tipo de dados base: **tinyint**|  
|Status|Status do banco de dados.|ONLINE: o banco de dados está disponível para consulta.<br /><br /> **Observação:** A função pode retornar um status ONLINE enquanto o banco de dados for aberto e ainda não tiver sido recuperado. Para identificar se um banco de dados ONLINE pode aceitar conexões, consulte a propriedade Ordenação de **DATABASEPROPERTYEX**. O banco de dados ONLINE pode aceitar conexões quando a ordenação de banco de dados retorna um valor não nulo. Para bancos de dados Always On, consulte as colunas database_state ou database_state_desc de `sys.dm_hadr_database_replica_states`.<br /><br /> OFFLINE: o banco de dados foi colocado em offline explicitamente.<br /><br /> RESTORING: a restauração de banco de dados foi iniciada.<br /><br /> RECOVERING: a recuperação do banco de dados foi iniciada e o banco de dados ainda não está pronto para consultas.<br /><br /> SUSPECT: o banco de dados não foi recuperado.<br /><br /> EMERGENCY: o banco de dados está em uma emergência, em estado somente leitura. O acesso está restrito a membros sysadmin<br /><br /> Tipo de dados base: **nvarchar(128)**|  
|Updateability|Indica se os dados podem ser modificados.|READ_ONLY: o banco de dados dá suporte a leituras de dados, mas não a modificações de dados.<br /><br /> READ_WRITE: o banco de dados dá suporte a leituras e a modificações de dados.<br /><br /> Tipo de dados base: **nvarchar(128)**|  
|UserAccess|Indica quais usuários podem acessar o banco de dados.|SINGLE_USER: apenas um usuário db_owner, dbcreator ou sysadmin por vez<br /><br /> RESTRICTED_USER: apenas membros das funções db_owner, dbcreator ou sysadmin<br /><br /> MULTI_USER: todos os usuários<br /><br /> Tipo de dados base: **nvarchar(128)**|  
|Versão|Número de versão interno do código [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com que o banco de dados foi criado. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|Número de versão: o banco de dados está aberto.<br /><br /> NULL: o banco de dados não foi iniciado.<br /><br /> Tipo de dados base: **int**| 

<br/>   

> [!NOTE]  
> <sup>1</sup> Para bancos de dados que fazem parte de um grupo de disponibilidade, `LastGoodCheckDbTime` retornará a data e hora do último DBCC CHECKDB bem-sucedido executado na réplica primária, independentemente da réplica da qual você está executando o comando. 

## <a name="return-types"></a>Tipos de retorno
**sql_variant**
  
## <a name="exceptions"></a>Exceções  
Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.
  
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário só pode exibir os metadados de itens protegíveis de sua propriedade ou para os quais ele tenha permissão concedida. Isso significa que as funções internas que emitem metadados, como `OBJECT_ID`, poderão retornar NULL se o usuário não tiver permissões para o objeto. Veja [Configuração de Visibilidade de Metadados](../../relational-databases/security/metadata-visibility-configuration.md) para obter mais informações.
  
## <a name="remarks"></a>Comentários  
`DATABASEPROPERTYEX` retorna somente uma configuração de propriedade por vez. Para exibir várias configurações de propriedade, use a exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-the-status-of-the-auto_shrink-database-option"></a>a. Recuperando o estado da opção de banco de dados AUTO_SHRINK  
Este exemplo retorna o status da opção de banco de dados AUTO_SHRINK para o banco de dados `AdventureWorks`.
  
```sql
SELECT DATABASEPROPERTYEX('AdventureWorks2014', 'IsAutoShrink');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)] Isso indica que AUTO_SHRINK está desativada.
  
```sql
------------------  
0  
```  
  
### <a name="b-retrieving-the-default-collation-for-a-database"></a>B. Recuperando a ordenação padrão de um banco de dados  
Este exemplo retorna vários atributos do banco de dados `AdventureWorks`.
  
```sql
SELECT   
    DATABASEPROPERTYEX('AdventureWorks2014', 'Collation') AS Collation,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'Edition') AS Edition,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'ServiceObjective') AS ServiceObjective,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'MaxSizeInBytes') AS MaxSizeInBytes  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Collation                     Edition        ServiceObjective  MaxSizeInBytes  
----------------------------  -------------  ----------------  --------------  
SQL_Latin1_General_CP1_CI_AS  DataWarehouse  DW1000            5368709120  
```  
  
## <a name="see-also"></a>Confira também
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[Estados de banco de dados](../../relational-databases/databases/database-states.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)
  
  
