---
title: DATABASEPROPERTYEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a67b74ad595fdf7b6f3a63dbd2ea2c9e5793f54f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="databasepropertyex-transact-sql"></a>DATABASEPROPERTYEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna a configuração atual da opção ou propriedade de banco de dados especificada para o banco de dados especificado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATABASEPROPERTYEX ( database , property )  
```  
  
## <a name="arguments"></a>Argumentos  
*database*  
É uma expressão que representa o nome do banco de dados para o qual retornar as informações da propriedade nomeada. *database* é **nvarchar(128)**.  
Para [!INCLUDE[ssSDS](../../includes/sssds-md.md)], deve ser o nome do banco de dados atual. Retorna NULL para todas as propriedades se for fornecido um nome de banco de dados diferente.
  
*property*  
É uma expressão que representa o nome da propriedade do banco de dados a ser retornada. *property* é **varchar(128)** e pode ser um dos valores a seguir. O tipo de retorno é **sql_variant**. A tabela a seguir mostra o tipo de dados base para obter cada valor de propriedade.
  
> [!NOTE]  
>  Se o banco de dados não for iniciado, as propriedades que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recupera acessando o banco de dados diretamente em vez de recuperar o valor de metadados retornarão NULL. Ou seja, se o banco de dados tiver AUTO_CLOSE definido como ON ou, caso contrário, o banco de dados está offline.  
  
|Propriedade|Description|Valor retornado|  
|---|---|---|
|Agrupamento|O nome do agrupamento padrão para o banco de dados.|Nome do agrupamento<br /><br /> NULL = Banco de dados não foi iniciado.<br /><br /> Tipo de dados base: **nvarchar(128)**|  
|ComparisonStyle|O estilo de comparação do agrupamento do Windows. ComparisonStyle é um bitmap calculado com os valores a seguir para os possíveis estilos.<br /><br /> Ignorar maiúsculas e minúsculas: 1<br /><br /> Ignorar acento: 2<br /><br /> Ignorar Kana: 65536<br /><br /> Ignorar largura: 131072<br /><br /> <br /><br /> Por exemplo, o padrão de 196609 é o resultado de combinar as opções Ignorar maiúsculas e minúsculas, Ignorar Kana e Ignorar largura.|Retorna o estilo de comparação.<br /><br /> Retorna 0 para todos os agrupamentos binários.<br /><br /> Tipo de dados base: **int**|  
|Edição|A camada de edição ou de serviço do banco de dados.|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].<br /><br /> <br /><br /> Web = Banco de Dados Web Edition<br /><br /> Negócios = Banco de Dados Business Edition<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium<br /><br /> Sistema (para o banco de dados mestre)<br /><br /> NULL = Banco de dados não foi iniciado.<br /><br /> Tipo de dados base: **nvarchar**(64)|  
|IsAnsiNullDefault|O banco de dados segue regras de ISO por permitir valores nulos.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsAnsiNullsEnabled|Todas as comparações com um nulo são avaliadas como desconhecido.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsAnsiPaddingEnabled|As cadeias de caracteres são convertidas na mesma largura antes da comparação ou inserção.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsAnsiWarningsEnabled|Mensagens de erro ou de aviso são emitidas quando ocorrem condições de erro padrão.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsArithmeticAbortEnabled|Consultas são encerradas quando um erro de estouro ou divisão por zero ocorre durante a execução da consulta.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsAutoClose|O banco de dados é desligado corretamente e libera recursos depois da saída do último usuário.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsAutoCreateStatistics|O otimizador de consulta cria estatísticas de coluna única, conforme necessário, para melhorar o desempenho de consulta.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsAutoCreateStatisticsIncremental|As estatísticas e coluna única criadas automaticamente são incrementais quando possível.|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsAutoShrink|Os arquivos de banco de dados são candidatos à redução automática periódica.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsAutoUpdateStatistics|O otimizador de consulta atualiza estatísticas existentes quando elas são usadas por uma consulta, podendo ficar desatualizadas.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|
|IsClone|Banco de dados é uma cópia somente de esquema e estatísticas de um banco de dados do usuário.|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2.<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**| 
|IsCloseCursorsOnCommitEnabled|Os cursores que estão abertos quando uma transação é confirmada são fechados.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsFulltextEnabled|O banco de dados está habilitado para indexação de texto completo e semântica.|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**<br /><br /> **Observação:** o valor dessa propriedade não tem nenhum efeito. Os bancos de dados de usuário são sempre habilitados para pesquisa de texto completo. Essa coluna será removida em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não a utilize em novos desenvolvimentos e, assim que possível, modifique os aplicativos que atualmente utilizam alguma dessas colunas.|  
|IsInStandBy|O banco de dados está online como somente leitura, com o log de restauração permitido.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsLocalCursorsDefault|As declarações de cursor assumem LOCAL como padrão.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsMemoryOptimizedElevateToSnapshotEnabled|As tabelas com otimização de memória são acessadas usando o isolamento SNAPSHOT quando a configuração de sessão TRANSACTION ISOLATION LEVEL é definida como um nível de isolamento inferior, READ COMMITTED ou READ UNCOMMITTED.|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> Tipo de dados base: **int**|  
|IsMergePublished|As tabelas de um banco de dados podem ser publicadas por replicação de mesclagem, se a replicação tiver sido instalada.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsNullConcat|O operando de concatenação nulo resulta em NULL.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsNumericRoundAbortEnabled|Erros são gerados quando a perda de precisão ocorre em expressões.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsParameterizationForced|A opção SET de banco de dados PARAMETERIZATION é FORCED.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida|  
|IsQuotedIdentifiersEnabled|As aspas duplas só podem ser utilizadas em identificadores.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsPublished|As tabelas do banco de dados podem ser publicadas por instantâneo ou replicação transacional, se a replicação tiver sido instalada.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsRecursiveTriggersEnabled|O acionamento recursivo dos disparadores está habilitado.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsSubscribed|O banco de dados é assinado para uma publicação.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsSyncWithBackup|O banco de dados é um banco de dados publicado ou um banco de dados de distribuição e pode ser restaurado sem romper replicação transacional.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsTornPageDetectionEnabled|O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] detecta operações de E/S incompletas causadas por falhas de energia ou outros problemas no sistema.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada não válida<br /><br /> Tipo de dados base: **int**|  
|IsXTPSupported|Indica se o banco de dados dá suporte a OLTP in-memory, ou seja, criação e uso de tabelas com otimização de memória e módulos compilados nativamente.<br /><br /> Específico ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> IsXTPSupported não depende da existência de um grupo de arquivos MEMORY_OPTIMIZED_DATA, que é necessário para a criação de objetos OLTP in-memory.|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br /> **Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada inválida, um erro ou não aplicável<br /><br /> Tipo de dados base: **int**|  
|LCID|O identificador de localidade do Windows (LCID) do agrupamento.|Valor LCID (em formato decimal).<br /><br /> Tipo de dados base: **int**|  
|MaxSizeInBytes|Tamanho máximo do banco de dados em bytes.|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].<br /><br /> <br /><br /> 1073741824<br /><br /> 5368709120<br /><br /> 10737418240<br /><br /> 21474836480<br /><br /> 32212254720<br /><br /> 42949672960<br /><br /> 53687091200<br /><br /> NULL = Banco de dados não foi iniciado<br /><br /> Tipo de dados base: **bigint**|  
|Recuperação|Modelo de recuperação do banco de dados.|FULL = Modelo de recuperação completa<br /><br /> BULK_LOGGED = Modelo de log de transações em massa<br /><br /> SIMPLE = Modelo de recuperação simples<br /><br /> Tipo de dados base: **nvarchar(128)**|  
|ServiceObjective|Descreve o nível de desempenho do banco de dados no [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ou [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|Pode ser uma destas opções:<br /><br /> Nulo: banco de dados não iniciado<br /><br /> Compartilhado (para edições Web/Business)<br /><br /> Basic<br /><br /> S0<br /><br /> S1<br /><br /> S2<br /><br /> S3<br /><br /> P1<br /><br /> P2<br /><br /> P3<br /><br /> ElasticPool<br /><br /> Sistema (para o banco de dados mestre)<br /><br /> Tipo de dados base: **nvarchar(32)**|  
|ServiceObjectiveId|O id do objetivo de serviço em [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|**uniqueidentifier** que identifica o objetivo de serviço.|  
|SQLSortOrder|Identificação de ordem de classificação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com suporte em versões anteriores do SQL Server.|0 = Banco de dados está usando o agrupamento do Windows<br /><br /> >0 = ID da ordem de classificação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> NULL = Entrada não é válida ou banco de dados não foi iniciado<br /><br /> Tipo de dados base: **tinyint**|  
|Status|Status do banco de dados.|ONLINE = O banco de dados está disponível para consulta.<br /><br /> **Observação:** o status ONLINE pode ser retornado enquanto o banco de dados estiver sendo aberto e ainda não estiver recuperado. Para identificar quando um banco de dados pode aceitar conexões, consulte a propriedade **DATABASEPROPERTYEX**. O banco de dados pode aceitar conexões quando o agrupamento de banco de dados retorna um valor não nulo. Para bancos de dados Always On, consulte as colunas database_state ou database_state_desc de sys.dm_hadr_database_replica_states.<br /><br /> OFFLINE = Banco de dados foi colocado em offline explicitamente.<br /><br /> RESTORING = Banco de dados está sendo restaurado.<br /><br /> RECOVERING = Banco de dados está sendo recuperando e ainda não está pronto para consultas.<br /><br /> SUSPECT = Banco de dados não foi recuperado.<br /><br /> EMERGENCY = Banco de dados está em uma emergência, em estado somente leitura. O acesso está restrito a membros sysadmin<br /><br /> Tipo de dados base: **nvarchar(128)**|  
|Updateability|Indica se os dados podem ser modificados.|READ_ONLY = Dados podem ser lidos, mas não modificados.<br /><br /> READ_WRITE = Dados podem ser lidos e modificados.<br /><br /> Tipo de dados base: **nvarchar(128)**|  
|UserAccess|Indica quais usuários podem acessar o banco de dados.|SINGLE_USER = Apenas um usuário db_owner, dbcreator ou sysadmin de cada vez<br /><br /> RESTRICTED_USER = Apenas membros das funções db_owner, dbcreator e sysadmin<br /><br /> MULTI_USER = Todos os usuários<br /><br /> Tipo de dados base: **nvarchar(128)**|  
|Versão|Número de versão interno do código [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com que o banco de dados foi criado. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|Número de versão = Banco de dados está aberto.<br /><br /> NULL = Banco de dados não foi iniciado.<br /><br /> Tipo de dados base: **int**|  
  
## <a name="return-types"></a>Tipos de retorno
**sql_variant**
  
## <a name="exceptions"></a>Exceções  
Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.
  
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário só pode exibir os metadados de itens protegíveis de sua propriedade ou para os quais ele tenha permissão concedida. Isso significa que funções internas que emitem metadados, como OBJECT_ID, poderão retornar o NULL se o usuário não tiver nenhuma permissão para o objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).
  
## <a name="remarks"></a>Remarks  
DATABASEPROPERTYEX retorna somente uma configuração de propriedade de cada vez. Para exibir várias configurações de propriedade, use a exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-the-status-of-the-autoshrink-database-option"></a>A. Recuperando o estado da opção de banco de dados AUTO_SHRINK  
O exemplo a seguir retorna o status da opção de banco de dados AUTO_SHRINK para `AdventureWorks`.
  
```sql
SELECT DATABASEPROPERTYEX('AdventureWorks2014', 'IsAutoShrink');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)] Isso indica que AUTO_SHRINK está desativada.
  
```sql
------------------  
0  
```  
  
### <a name="b-retrieving-the-default-collation-for-a-database"></a>B. Recuperando o agrupamento padrão de um banco de dados  
O exemplo a seguir retorna vários atributos do banco de dados `AdventureWorks`.
  
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
  
## <a name="see-also"></a>Consulte também
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[Estados de banco de dados](../../relational-databases/databases/database-states.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)
  
  
