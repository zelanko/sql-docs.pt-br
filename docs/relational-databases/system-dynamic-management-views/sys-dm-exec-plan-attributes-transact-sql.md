---
title: sys. dm_exec_plan_attributes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_plan_attributes_TSQL
- dm_exec_plan_attributes_TSQL
- dm_exec_plan_attributes
- sys.dm_exec_plan_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_plan_attributes dynamic management function
ms.assetid: dacf3ab3-f214-482e-aab5-0dab9f0a3648
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7ffabc2f8bb48b006ec1224a3ae81ac49d6c21f0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734794"
---
# <a name="sysdm_exec_plan_attributes-transact-sql"></a>sys.dm_exec_plan_attributes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha por atributo de plano para o plano especificado pelo identificador de plano. Você pode usar esta função com valor de tabela para obter detalhes sobre um plano específico, como os valores chave de cache ou o número atual de execuções simultâneas do plano.  
  
> [!NOTE]  
>  Algumas das informações retornadas por essa função são mapeadas para a exibição de compatibilidade com versões anteriores do [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) .

## <a name="syntax"></a>Sintaxe  
```  
sys.dm_exec_plan_attributes ( plan_handle )  
```  
  
## <a name="arguments"></a>Argumentos  
 *plan_handle*  
 Identifica exclusivamente um plano de consulta de um lote que foi executado e cujo plano reside no cache de plano. *plan_handle* é **varbinary (64)**. O identificador de plano pode ser obtido na exibição de gerenciamento dinâmico [Sys. dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) .  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|Atributo|**varchar(128)**|O nome do atributo associado com este plano. A tabela imediatamente abaixo dessa lista os possíveis atributos, seus tipos de dados e suas descrições.|  
|value|**sql_variant**|Valor do atributo que é associado ao plano.|  
|is_cache_key|**bit**|Indica se o atributo é usado como parte da chave de consulta de cache para o plano.|  

Na tabela acima, o **atributo** pode ter os seguintes valores:

|Atributo|Tipo de dados|Descrição|  
|---------------|---------------|-----------------|  
|set_options|**int**|Indica os valores de opção com os quais o plano foi compilado.|  
|objectid|**int**|Uma das chaves principais usadas para pesquisar um objeto no cache. Essa é a ID de objeto armazenada em [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) para objetos de banco de dados (procedimentos, exibições, gatilhos e assim por diante). Para planos do tipo "Adhoc" ou "Preparado", é um hash interno do texto de lote.|  
|dbid|**int**|É o identificador do banco de dados que contém a entidade à qual o plano se refere.<br /><br /> Para planos ad hoc ou preparados, é o identificador do banco de dados da partir do qual o lote é executado.|  
|dbid_execute|**int**|Para objetos do sistema armazenados no banco de dados de **recursos** , a ID do banco de dados do qual o plano armazenado em cache é executado. 0 para todos os outros casos.|  
|user_id|**int**|Um valor de -2 indica que o lote enviado não depende da resolução de nome implícita e pode ser compartilhado entre usuários diferentes. Este é o método preferencial. Qualquer outro valor representa a identificação do usuário que submete a consulta no banco de dados.| 
|language_id|**smallint**|A identificação de idioma da conexão que criou o objeto de cache. Para obter mais informações, consulte [linguagens desys.sys&#40;&#41;Transact-SQL ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).|  
|date_format|**smallint**|O formato de data da conexão que criou o objeto de cache. Para obter mais informações, veja [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md).|  
|date_first|**tinyint**|Primeiro valor de data. Para obter mais informações, veja [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).|  
|status|**int**|Bits de status interno que fazem parte da chave de consulta do cache.|  
|required_cursor_options|**int**|Opções de cursor especificadas pelo usuário, como o tipo de cursor.|  
|acceptable_cursor_options|**int**|Opções de cursor que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode converter implicitamente para  aceitar a execução da instrução. Por exemplo, o usuário pode especificar um cursor dinâmico, mas o otimizador de consulta pode converter esse tipo de cursor para um cursor estático.|  
|inuse_exec_context|**int**|Número de lotes em execução que estão usando o plano de consulta.|  
|free_exec_context|**int**|Número de contextos de execução em cache do plano de consulta que não está sendo utilizado atualmente.|  
|hits_exec_context|**int**|Número de vezes que o contexto de execução foi obtido do cache de plano e  reutilizado,  economizando a sobrecarga de recompilar a instrução SQL. O valor é uma agregação de todas as execuções de lote até o momento.|  
|misses_exec_context|**int**|Número de vezes que não foi possível localizar um contexto de execução no cache de plano, resultando na criação de um contexto de execução novo para a execução de lote.|  
|removed_exec_context|**int**|Número de contextos de execução que foram removidos devido à pressão de memória no plano de cache.|  
|inuse_cursors|**int**|Número de lotes em execução que contêm um ou mais cursores que estão usando o plano de cache.|  
|free_cursors|**int**|Número de cursores inativos ou livres no plano de cache.|  
|hits_cursors|**int**|Número de vezes que um cursor inativo foi obtido do plano de cache e reutilizado. O valor é uma agregação de todas as execuções de lote até o momento.|  
|misses_cursors|**int**|Número de vezes que não foi possível localizar um cursor inativo no cache.|  
|removed_cursors|**int**|Número de cursores de que foram removidos devido à pressão de memória no plano de cache.|  
|sql_handle|**varbinary**(64)|O identificador SQL do lote.|  
|merge_action_type|**smallint**|O tipo de plano de execução de gatilho usado como o resultado de uma instrução MERGE.<br /><br /> 0 indica plano de não gatilho, um plano de gatilho não executado como o resultado de uma instrução MERGE ou um plano de gatilho executado como o resultado de uma instrução MERGE que só especifica uma ação DELETE.<br /><br /> 1 indica um plano de gatilho INSERT que executa como o resultado de uma instrução MERGE.<br /><br /> 2 indica um plano de gatilho UPDATE que executa como o resultado de uma instrução MERGE.<br /><br /> 3 indica um plano de gatilho DELETE que executa como o resultado de uma instrução MERGE  que contém uma ação INSERT ou UPDATE correspondente.<br /><br /> Para gatilhos aninhados executados por cascateamento de ações, este valor é a ação da instrução MERGE que causou a cascata.|  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="remarks"></a>Comentários  
  
## <a name="set-options"></a>Opções de configuração  
 As cópias do mesmo plano compilado podem diferir somente pelo valor na coluna **set_options** . Indica que conexões diferentes estão usando conjuntos diferentes de opções SET para a mesma consulta. Usar conjuntos diferentes de opções não é desejável, porque podem causar compilações extras, baixa reutilização de plano e inflação de cache do plano, devido a várias cópias de planos no cache.  
  
### <a name="evaluating-set-options"></a>Avaliando opções de configuração  
 Para converter o valor retornado em **set_options** às opções com as quais o plano foi compilado, subtraia os valores do valor de **set_options** , começando com o maior valor possível, até chegar a 0. Cada valor subtraído corresponde a uma opção que foi usada no plano de consulta. Por exemplo, se o valor em **set_options** for 251, as opções com as quais o plano foi compilado são ANSI_NULL_DFLT_ON (128), QUOTED_IDENTIFIER (64), ANSI_NULLS (32), ANSI_WARNINGS (16), CONCAT_NULL_YIELDS_NULL (8), plano paralelo (2) e ANSI_PADDING (1).  
  
|Opção|Valor|  
|------------|-----------|  
|ANSI_PADDING|1|  
|Plano paralelo|2|  
|FORCEPLAN|4|  
|CONCAT_NULL_YIELDS_NULL|8|  
|ANSI_WARNINGS|16|  
|ANSI_NULLS|32|  
|QUOTED_IDENTIFIER|64|  
|ANSI_NULL_DFLT_ON|128|  
|ANSI_NULL_DFLT_OFF|256|  
|NoBrowseTable<br /><br /> Indica que o plano não usa uma tabela de trabalho para implementar uma operação de FOR BROWSE.|512|  
|TriggerOneRow<br /><br /> Indica que o plano contém uma única otimização de linha para tabelas delta de gatilho AFTER.|1024|  
|ResyncQuery<br /><br /> Indica que a consulta foi submetida através de procedimentos armazenados do sistema interno.|2.048|  
|ARITH_ABORT|4096|  
|NUMERIC_ROUNDABORT|8192|  
|DATEFIRST|16384|  
|DATEFORMAT|32768|  
|LanguageID|65536|  
|UPON<br /><br /> Indica que a opção de banco de dados PARAMETERIZATION foi definida como FORCED quando o plano foi compilado.|131072|  
|ROWCOUNT|**Aplica-se a:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Para[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /><br /> 262144|  
  
## <a name="cursors"></a>Cursores  
 Cursores inativos são colocados em cache em um plano compilado de forma que a memória usada para armazenar o cursor pode ser usada de novo por usuários simultâneos de cursores. Por exemplo, suponha que um lote declara e usa um cursor sem desalocá-lo. Se houver dois usuários executando o mesmo lote, haverá dois cursores ativos. Quando os cursores são desalocados (potencialmente em lotes diferentes), a memória usada para armazenar o cursor é gravada em cache e não é liberada. Esta lista de cursores inativos é mantida no plano compilado. Na próxima vez que um usuário executar o lote, a memória de cursor em cache será usada novamente e inicializada adequadamente como um cursor ativo.  
  
### <a name="evaluating-cursor-options"></a>Avaliando opções de cursor  
 Para converter o valor retornado em **required_cursor_options** e **acceptable_cursor_options** às opções com as quais o plano foi compilado, subtraia os valores do valor da coluna, começando com o maior valor possível, até chegar a 0. Cada valor subtraído corresponde a uma opção cursor que foi usada no plano de consulta.  
  
|Opção|Valor|  
|------------|-----------|  
|Nenhum|0|  
|INSENSITIVE|1|  
|SCROLL|2|  
|READ ONLY|4|  
|FOR UPDATE|8|  
|LOCAL|16|  
|GLOBAL|32|  
|FORWARD_ONLY|64|  
|KEYSET|128|  
|DYNAMIC|256|  
|SCROLL_LOCKS|512|  
|OPTIMISTIC|1024|  
|STATIC|2.048|  
|FAST_FORWARD|4096|  
|IN PLACE|8192|  
|FOR *select_statement*|16384|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-attributes-for-a-specific-plan"></a>a. Retornando os atributos de um plano específico  
 O exemplo a seguir retorna todos os atributos de um plano específico. A exibição de gerenciamento dinâmico  `sys.dm_exec_cached_plans` é consultada primeiro para obter o identificador para o plano especificado. Na segunda consulta, substitua o `<plan_handle>` por  um valor de identificador de plano da primeira consulta.  
  
```sql  
SELECT plan_handle, refcounts, usecounts, size_in_bytes, cacheobjtype, objtype   
FROM sys.dm_exec_cached_plans;  
GO  
SELECT attribute, value, is_cache_key  
FROM sys.dm_exec_plan_attributes(<plan_handle>);  
GO  
```  
  
### <a name="b-returning-the-set-options-for-compiled-plans-and-the-sql-handle-for-cached-plans"></a>B. Retornando as opções SET para planos compilados e a o identificador SQL para planos em cache  
 O exemplo a seguir retorna um valor que representa as opções com as quais cada plano foi compilado. Além disso, o identificador SQL para todos os planos em cache é retornado.  
  
```sql  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
    SELECT plan_handle, epa.attribute, epa.value   
    FROM sys.dm_exec_cached_plans   
        OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
    WHERE cacheobjtype = 'Compiled Plan') AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys. dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  

