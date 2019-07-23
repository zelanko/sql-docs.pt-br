---
title: Dicas de consulta (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Query_Hint_TSQL
- Query_TSQL
- Query
- Query Hint
- MAX_GRANT_PERCENT
- MAX_GRANT_PERCENT_TSQL
- MIN_GRANT_PERCENT
- MIN_GRANT_PERCENT_TSQL
- EXTERNALPUSHDOWN
- EXTERNALPUSHDOWN_TSQL
- NOLOCK_TSQL
- MAXDOP_TSQL
- USE_HINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REPORT PLAN query hint
- FORCE ORDER query hint
- HASH JOIN query hint
- query hints [SQL Server]
- OPTIMIZE FOR query hint
- FORCESCAN query hint
- RECOMPILE query hint
- MAXRECURSION query hint
- MERGE JOIN query hint
- HASH GROUP query hint
- KEEP PLAN query hint
- UNION query hint
- FORCESEEK query hint
- ORDER GROUP query hint
- LOOP JOIN query hint
- KEEPFIXED PLAN query hint
- FAST query hint
- MAXDOP query hint
- PARAMETERIZATION query hint
- hints [SQL Server], query
- JOIN query hint
- USE PLAN query hint
- EXPAND VIEWS query hint
- MAX_GRANT_PERCENT query hint
- MIN_GRANT_PERCENT query hint
- EXTERNALPUSHDOWN query hint
- USE HINT query hint
- QUERY_PLAN_PROFILE query hint
ms.assetid: 66fb1520-dcdf-4aab-9ff1-7de8f79e5b2d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6e319fb56760f78df56105873f26a9bbec004dd6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902009"
---
# <a name="hints-transact-sql---query"></a>Dicas (Transact-SQL) – consulta
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

As dicas de consulta especificam que as dicas indicadas devem ser usadas em toda a consulta. Elas afetam todos os operadores na instrução. Se UNION estiver envolvida na consulta principal, só a última consulta envolvendo uma operação UNION poderá ter a cláusula OPTION. As dicas de consulta são especificadas como parte da [cláusula OPTION](../../t-sql/queries/option-clause-transact-sql.md). O Erro 8622 ocorrerá se uma ou mais dicas de consulta fizerem com que o otimizador de consulta não gere um plano válido.  
  
> [!CAUTION]  
> Como o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleciona, normalmente, o melhor plano de execução para uma consulta, recomendamos usar dicas apenas como último recurso para desenvolvedores e administradores de banco de dados experientes.  
  
**Aplica-se a:**  
  
[DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
[INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
[SELECT](../../t-sql/queries/select-transact-sql.md)  
  
[UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
[MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<query_hint > ::=   
{ { HASH | ORDER } GROUP   
  | { CONCAT | HASH | MERGE } UNION   
  | { LOOP | MERGE | HASH } JOIN   
  | EXPAND VIEWS   
  | FAST number_rows   
  | FORCE ORDER   
  | { FORCE | DISABLE } EXTERNALPUSHDOWN  
  | IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
  | KEEP PLAN   
  | KEEPFIXED PLAN  
  | MAX_GRANT_PERCENT = percent  
  | MIN_GRANT_PERCENT = percent  
  | MAXDOP number_of_processors   
  | MAXRECURSION number   
  | NO_PERFORMANCE_SPOOL   
  | OPTIMIZE FOR ( @variable_name { UNKNOWN | = literal_constant } [ , ...n ] )  
  | OPTIMIZE FOR UNKNOWN  
  | PARAMETERIZATION { SIMPLE | FORCED }   
  | RECOMPILE  
  | ROBUST PLAN   
  | USE HINT ( '<hint_name>' [ , ...n ] )
  | USE PLAN N'xml_plan'  | TABLE HINT ( exposed_object_name [ , <table_hint> [ [, ]...n ] ] )  
}  
  
<table_hint> ::=  
[ NOEXPAND ] {   
    INDEX ( index_value [ ,...n ] ) | INDEX = ( index_value )  
  | FORCESEEK [( index_value ( index_column_name [,... ] ) ) ]  
  | FORCESCAN  
  | HOLDLOCK   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | READUNCOMMITTED   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT  
  | SPATIAL_WINDOW_MAX_CELLS = integer  
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK  
}  
```  
  
## <a name="arguments"></a>Argumentos  
{ HASH | ORDER } GROUP  
Especifica que as agregações que a cláusula GROUP BY ou DISTINCT da consulta descreve devem usar hash ou ordenação.  
  
{ MERGE | HASH | CONCAT } UNION  
Especifica que todas as operações UNION são executadas por mesclagem, hash ou concatenação de conjuntos de UNION. Se mais de uma dica de UNION for especificada, o otimizador de consulta selecionará a estratégia menos cara dentre as dicas especificadas.  
  
{ LOOP | MERGE | HASH } JOIN  
Especifica que todas as operações de junção são executadas por LOOP JOIN, MERGE JOIN ou HASH JOIN na consulta inteira. Se você especificar mais de uma dica de junção, o otimizador selecionará a estratégia de junção menos cara dentre as permitidas.  
  
Se você especificar uma dica de junção na cláusula FROM da mesma consulta para um par de tabelas específico, essa dica de junção terá precedência na junção das duas tabelas. As dicas de consulta, no entanto, ainda devem ser respeitadas. A dica de junção para o par de tabelas pode restringir apenas a seleção dos métodos de junção permitidos na dica de consulta. Para obter mais informações, consulte [Dicas de junção &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-join.md).  
  
EXPAND VIEWS  
Especifica que as exibições indexadas são expandidas. Também especifica que o otimizador de consulta não considera qualquer exibição indexada como uma substituição de qualquer bloco da consulta. Uma exibição é expandida quando sua definição substitui o seu nome no texto da consulta.  
  
Esta dica de consulta desabilita o uso direto de exibições indexadas e índices em exibições indexadas no plano de consulta.  
  
A exibição indexada permanecerá condensada se houver uma referência direta à exibição no bloco SELECT da consulta. A exibição também permanecerá condensada se você especificar WITH (NOEXPAND) ou WITH (NOEXPAND, INDEX(index\_value_ [ **,** _...n_ ] ) ). Para obter mais informações sobre a dica de consulta NOEXPAND, confira [Usando NOEXPAND](../../t-sql/queries/hints-transact-sql-table.md#using-noexpand).  
  
A dica afetará apenas as exibições no bloco SELECT das instruções, incluindo as exibições nas instruções INSERT, UPDATE, MERGE e DELETE.  
  
FAST _number\_rows_  
Especifica que a consulta é otimizada para recuperação rápida das primeiras _number\_rows_. Esse resultado é um inteiro não negativo. Depois que as primeiras _number\_rows_ são retornadas, a consulta continua a execução e produz seu conjunto de resultados completo.  
  
FORCE ORDER  
Especifica que a ordem de junção indicada pela sintaxe de consulta é preservada durante a otimização da consulta. Usar FORCE ORDER não afeta o possível comportamento de reversão de função do otimizador de consulta.  
  
> [!NOTE]  
> Em uma instrução MERGE, a tabela de origem é acessada antes da tabela de destino como a ordem de junção padrão, a menos que a cláusula WHEN SOURCE NOT MATCHED seja especificada. Especificar FORCE ORDER preserva esse comportamento padrão.  
  
{ FORCE | DISABLE } EXTERNALPUSHDOWN  
Forçar ou desabilitar o pushdown da computação de expressões qualificadas no Hadoop. Aplica-se somente a consultas que usam PolyBase. Não se aplicará ao armazenamento do Azure.  
  
KEEP PLAN  
Força o otimizador de consulta a relaxar o limite de recompilação estimado para uma consulta. O limite de recompilação estimado inicia uma recompilação automática para a consulta quando o número estimado de alterações na coluna indexada é feito em uma tabela com a execução de uma das seguintes instruções:

* UPDATE
* Delete (excluir)
* MERGE
* INSERT

Especificar KEEP PLAN assegura que uma consulta não seja recompilada tão frequentemente como quando há várias atualizações em uma tabela.  
  
KEEPFIXED PLAN  
Força o otimizador de consulta a não recompilar uma consulta devido às alterações nas estatísticas. Especificar KEEPFIXED PLAN garantirá que uma consulta seja recompilada apenas se o esquema das tabelas subjacentes for alterado ou se **sp_recompile** for executado nessas tabelas.  
  
IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Impede a consulta de usar um índice columnstore otimizado para memória não clusterizado. Se a consulta contiver a dica de consulta para evitar o uso do índice columnstore e uma dica de índice para usar um índice columnstore, as dicas entrarão em conflito e a consulta retornará um erro.  
  
MAX_GRANT_PERCENT = _percent_  
O tamanho máximo de concessão de memória em PERCENT. É garantido que a consulta não excederá esse limite. O limite real poderá ser inferior se a configuração do Resource Governor for mais baixa que o valor especificado por esta dica. Os valores válidos estão entre 0,0 e 100,0.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
MIN_GRANT_PERCENT = _percent_  
Tamanho mínimo de concessão de memória em PERCENT = % do limite padrão. É garantido que a consulta obtenha o MAX (memória necessária, mínima concedida) porque é preciso pelo menos a memória necessária para iniciar uma consulta. Os valores válidos estão entre 0,0 e 100,0.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
MAXDOP _number_  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Substitui a opção de configuração de **grau máximo de paralelismo** de **sp_configure**. Também substitui o Resource Governor para a consulta que especifica essa opção. A dica de consulta MAXDOP pode exceder o valor configurado com sp_configure. Se MAXDOP exceder o valor configurado com o Resource Governor, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usará o valor de MAXDOP do Resource Governor, descrito em [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md). Todas as regras semânticas usadas com a opção de configuração **max degree of parallelism** são aplicáveis ao usar a dica de consulta MAXDOP. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
  
> [!WARNING]     
> Se MAXDOP estiver definido como 0, o servidor escolherá o máximo grau de paralelismo.  
  
MAXRECURSION _number_     
Especifica o número máximo de recursões permitidas para esta consulta. _number_ é um inteiro não negativo entre 0 e 32.767. Quando 0 é especificado, nenhum limite é aplicado. Se essa opção não for especificada, o limite padrão para o servidor será de 100.  
  
Quando o número especificado ou padrão de limite de MAXRECURSION é atingido durante a execução da consulta, a consulta é encerrada e um erro é retornado.  
  
Por causa desse erro, todos os efeitos da instrução são revertidos. Se a instrução for do tipo SELECT, poderão ser retornados resultados parciais ou nenhum resultado. Eventuais resultados parciais retornados podem não incluir todas as linhas em níveis de recursão acima do nível de recursão máximo especificado.  
  
Para obter mais informações, confira [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).     
  
NO_PERFORMANCE_SPOOL    
 **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Impede que um operador de spool seja adicionado aos planos de consulta (exceto para os planos em que o spool é necessário para assegurar uma semântica de atualização válida). O operador de spool pode reduzir o desempenho em alguns cenários. Por exemplo, o spool usa o tempdb e a contenção do tempdb pode ocorrer se houver várias consultas simultâneas em execução com as operações de spool.  
  
OPTIMIZE FOR ( _@variable\_name_ { UNKNOWN | = _literal\_constant }_ [ **,** ..._n_ ] )     
Instrui o otimizador de consulta a usar um valor específico para uma variável local quando a consulta é compilada e otimizada. O valor é usado somente durante a otimização da consulta e não durante sua execução.  
  
_@variable\_name_  
É o nome de uma variável local usada em uma consulta para a qual um valor pode ser atribuído para uso com a dica de consulta OPTIMIZE FOR.  
  
_UNKNOWN_  
Especifica que o otimizador de consulta usa dados estatísticos em vez do valor inicial para determinar o valor de uma variável local durante a otimização da consulta.  
  
_literal\_constant_  
É um valor constante literal a receber _@variable\_name_ para uso com a dica de consulta OPTIMIZE FOR. _literal\_constant_ é usado somente durante a otimização de consulta, e não como o valor de _@variable\_name_ durante a execução da consulta. _literal\_constant_ pode ser de um dos tipos de dados de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que pode ser expresso como uma constante literal. O tipo de dados de _literal\_constant_ precisa ser implicitamente conversível no tipo de dados que _@variable\_name_ faz referências na consulta.  
  
OPTIMIZE FOR pode anular o comportamento de detecção de parâmetro padrão do otimizador. Use OPTIMIZE FOR também quando criar guias de plano. Para obter mais informações, confira [Recompilar um procedimento armazenado](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md).  
  
OPTIMIZE FOR UNKNOWN  
Instrui o otimizador de consulta a usar dados estatísticos no lugar dos valores iniciais para todas as variáveis locais quando a consulta é compilada e otimizada. Essa otimização inclui parâmetros criados com parametrização forçada.  
  
Se você usar OPTIMIZE FOR @variable_name = _literal\_constant_ e OPTIMIZE FOR UNKNOWN na mesma dica de consulta, o otimizador de consulta usará a _literal\_constant_ especificada para um valor específico. O otimizador de consulta usará UNKNOWN para o restante dos valores de variável. Os valores só são usados durante a otimização de consulta e não durante a execução das consultas.  
  
PARAMETERIZATION { SIMPLE | FORCED }     
Especifica as regras de parametrização que o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica à consulta quando ela é compilada.  
  
> [!IMPORTANT]  
> A dica de consulta PARAMETERIZATION só pode ser especificada dentro de um guia de plano para substituir a configuração atual da opção SET do banco de dados PARAMETERIZATION. Ela não pode ser especificada diretamente dentro de uma consulta.    
> Para obter mais informações, confira [Especificar comportamento de parametrização de consulta usando guias de plano](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md).
  
SIMPLE instrui o otimizador de consulta a tentar parametrização simples. FORCED instrui o otimizador de consulta a tentar a parametrização forçada. Para obter mais informações, consulte [Parametrização forçada no Guia de arquitetura de processamento de consulta](../../relational-databases/query-processing-architecture-guide.md#ForcedParam) e [Parametrização simples no Guia de arquitetura de processamento de consulta](../../relational-databases/query-processing-architecture-guide.md#SimpleParam).  

RECOMPILE  
Instrui o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] a gerar um plano novo e temporário para a consulta e descartar esse plano imediatamente depois que a consulta conclui a execução. O plano de consulta gerado não substitui um plano armazenado em cache quando a mesma consulta é executada sem a dica RECOMPILE. Sem especificar RECOMPILE, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena em cache os planos de consulta e reutiliza-os. Ao compilar planos de consulta, a dica de consulta RECOMPILE usa os valores atuais de todas as variáveis locais na consulta. Se a consulta estiver em um procedimento armazenado, os valores atuais são passados para quaisquer parâmetros.  
  
RECOMPILE é uma alternativa útil para criar um procedimento armazenado. RECOMPILE usa a cláusula WITH RECOMPILE quando apenas um subconjunto de consultas dentro do procedimento armazenado, em vez de todo o procedimento armazenado, deve ser recompilado. Para obter mais informações, confira [Recompilar um procedimento armazenado](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md). RECOMPILE também é útil para a criação de guias de plano.  
  
ROBUST PLAN  
Força o otimizador de consulta a tentar um plano que trabalhe para o tamanho máximo de linhas potenciais, possivelmente às custas do desempenho. Tabelas e operadores intermediários podem ter que armazenar e processar linhas maiores do que qualquer uma das linhas de entrada quando a consulta é processada. As linhas podem ser tão grandes que, às vezes, o operador específico não consegue processá-las. Se as linhas tiverem essa dimensão, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] produzirá um erro durante a execução da consulta. Usar ROBUST PLAN, você instrui o otimizador de consulta a não considerar os plano de consulta que possam resultar nesse problema.  
  
Se um plano não for possível, o otimizador de consulta retornará um erro, em vez de adiar a detecção de erros para a execução da consulta. Linhas podem conter colunas de tamanho variável. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] permite definir linhas com o tamanho potencial máximo para além da capacidade de processamento do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Geralmente, apesar do tamanho potencial máximo, um aplicativo armazena linhas cujos tamanhos reais estão dentro dos limites de processamento do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] encontrar uma linha longa demais, será retornado um erro de execução.  
 
<a name="use_hint"></a> USE HINT ( **'** _hint\_name_ **'** )    
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
 
Fornece uma ou mais dicas adicionais ao processador de consultas. As dicas adicionais são especificadas por um nome de dica **entre aspas simples**.   

Os seguintes nomes de dica são compatíveis:    
 
*  'ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS' <a name="use_hint_join_containment"></a>       
   Faz o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerar um plano de consulta usando a suposição de Confinamento simples, em vez da suposição de Confinamento de base padrão para junções, no modelo de [Estimativa de cardinalidade](../../relational-databases/performance/cardinality-estimation-sql-server.md) do otimizador de consulta do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou mais recente. O nome da dica é equivalente ao [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9476. 
*  'ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES' <a name="use_hint_correlation"></a>      
   Faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gere um plano usando a seletividade mínima ao estimar predicados AND para os filtros a serem considerados para correlação. O nome da dica é equivalente ao [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4137 quando usado com o modelo de estimativa de cardinalidade do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e com versões anteriores, além disso, tem um efeito semelhante quando o [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9471 é usado com o modelo de estimativa de cardinalidade do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou superior.
*  'DISABLE_BATCH_MODE_ADAPTIVE_JOINS'       
   Desabilita junções adaptáveis do modo de lote. Para obter mais informações, confira [Junções Adaptáveis de modo de lote](../../relational-databases/performance/intelligent-query-processing.md#batch-mode-adaptive-joins). **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   
*  'DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK'       
   Desabilita os comentários de concessão de memória do modo de lote. Para obter mais informações, veja [Batch mode memory grant feedback](../../relational-databases/performance/intelligent-query-processing.md#batch-mode-memory-grant-feedback) (Comentários de concessão de memória de modo de lote). **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   
* 'DISABLE_DEFERRED_COMPILATION_TV'    
  Desabilita a compilação adiada de variável da tabela. Para saber mais, veja [Compilação adiada de variável da tabela](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation). **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   
*  'DISABLE_INTERLEAVED_EXECUTION_TVF'      
   Desabilita a execução intercalada para funções com valor de tabela de várias instruções. Para saber mais, veja [Execução intercalada para funções com valor de tabela de várias instruções](../../relational-databases/performance/intelligent-query-processing.md#interleaved-execution-for-mstvfs). **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   
*  'DISABLE_OPTIMIZED_NESTED_LOOP'      
   Instrui o processador de consultas a não usar uma operação de classificação (classificação em lote) para junções otimizadas de loops aninhados ao gerar um plano de consulta. O nome da dica é equivalente ao [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2340.
*  'DISABLE_OPTIMIZER_ROWGOAL' <a name="use_hint_rowgoal"></a>      
   Faz com que o SQL Server gere um plano que não usa as modificações de meta de linha com consultas que contêm estas palavras-chave: 
   
   * INÍCIO
   * OPTION (FAST N)
   * IN
   * EXISTS
   
   O nome da dica é equivalente ao [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4138.
*  'DISABLE_PARAMETER_SNIFFING'      
   Instrui o otimizador de consulta a usar a distribuição média de dados durante a compilação de uma consulta com um ou mais parâmetros. Essa instrução cria o plano de consulta independentemente do valor de parâmetro que foi usado pela primeira vez quando a consulta foi compilada. O nome da dica é equivalente ao [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4136 ou à definição `PARAMETER_SNIFFING = OFF` da [Configuração de Escopo do Banco de Dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
* 'DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK'    
  Desabilita os comentários de concessão de memória do modo de linha. Para obter mais informações, veja [Batch mode memory grant feedback](../../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback) (Comentários de concessão de memória de modo de lote). **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].     
* 'DISABLE_TSQL_SCALAR_UDF_INLINING'    
  Desabilita o embutimento de UDF escalar. Para saber mais, confira [Scalar UDF Inlining](../../relational-databases/user-defined-functions/scalar-udf-inlining.md) (Embutimento de UDF escalar). **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]).    
* 'DISALLOW_BATCH_MODE'    
  Desabilita a execução do modo de lote. Para obter mais informações, consulte [Modos de execução](../../relational-databases/query-processing-architecture-guide.md#execution-modes). **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].     
*  'ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS'      
   Habilita as estatísticas rápidas geradas automaticamente (aditamento de histograma) para qualquer coluna de índice inicial para a qual a estimativa de cardinalidade seja necessária. O histograma usado para estimar a cardinalidade será ajustado no tempo de compilação da consulta para considerar o valor máximo ou mínimo real dessa coluna. O nome da dica é equivalente ao [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4139. 
*  'ENABLE_QUERY_OPTIMIZER_HOTFIXES'     
   Habilita hotfixes do otimizador de consulta (alterações liberadas nas atualizações cumulativas do SQL Server e nos Service Packs). O nome da dica é equivalente ao [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4199 ou à definição `QUERY_OPTIMIZER_HOTFIXES = ON` da [Configuração de Escopo do Banco de Dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
*  'FORCE_DEFAULT_CARDINALITY_ESTIMATION'      
   Força o otimizador de consulta a usar o modelo de [estimativa de cardinalidade](../../relational-databases/performance/cardinality-estimation-sql-server.md) que corresponde ao nível de compatibilidade do banco de dados atual. Use essa dica para substituir a definição `LEGACY_CARDINALITY_ESTIMATION = ON` da [Configuração de Escopo do Banco de Dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) ou o [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481.
*  'FORCE_LEGACY_CARDINALITY_ESTIMATION' <a name="use_hint_ce70"></a>      
   Força o otimizador de consulta a usar o modelo de [estimativa de cardinalidade](../../relational-databases/performance/cardinality-estimation-sql-server.md) do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e de versões anteriores. O nome da dica é equivalente ao [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481 ou à definição `LEGACY_CARDINALITY_ESTIMATION = ON` da [Configuração de Escopo do Banco de Dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
*  'QUERY_OPTIMIZER_COMPATIBILITY_LEVEL_n'          
 Força o comportamento do otimizador de consulta em um nível de consulta. Esse comportamento ocorrerá se a consulta foi compilada com o nível de compatibilidade do banco de dados _n_, onde _n_ é um nível de compatibilidade do banco de dados com suporte. Confira [sys.dm_exec_valid_use_hints](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) para obter uma lista atual de valores com suporte para _n_. **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU10).    

   > [!NOTE]
   > A dica QUERY_OPTIMIZER_COMPATIBILITY_LEVEL_n não substituirá a configuração de estimativa de cardinalidade padrão ou herdada se ela for forçada pela configuração de escopo do banco de dados, pelo sinalizador de rastreamento ou por outra dica de consulta, como QUERYTRACEON.   
   > Essa dica só afeta o comportamento do otimizador de consulta. Ela não afeta outros recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que podem depender do [nível de compatibilidade do banco de dados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md), como a disponibilidade de determinados recursos de banco de dados.  
   > Para saber mais sobre essa dica, confira [Escolha do desenvolvedor: dicas do modelo de execução de consulta](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-hinting-query-execution-model).
    
*  'QUERY_PLAN_PROFILE'      
 Permite a criação de perfil leve para a consulta. Quando uma consulta que contém essa nova dica é concluída, um novo Evento Estendido, query_plan_profile, é disparado. Esse evento estendido expõe as estatísticas de execução e o plano de execução real XML semelhante ao evento estendido query_post_execution_showplan, mas apenas para consultas que contêm a nova dica. **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU3 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU11). 

   > [!NOTE]
   > Se você habilitar a coleta de evento estendido query_post_execution_showplan, isso adicionará a infraestrutura de criação de perfil padrão a cada consulta que esteja sendo executada no servidor e, portanto, poderá afetar o desempenho geral do servidor.      
   > Se você habilitar a coleção do evento estendido *query_thread_profile* para usar infraestrutura de criação de perfil leve, isso resultará em muito menos sobrecarga de desempenho, mas ainda afetará o desempenho geral do servidor.       
   > Se você habilitar o evento estendido de query_plan_profile, isso só habilitará a infraestrutura de criação de perfil leve para uma consulta executada com QUERY_PLAN_PROFILE, portanto, não afetará outras cargas de trabalho no servidor. Use essa dica para criar o perfil de uma consulta específica sem afetar outras partes da carga de trabalho do servidor.
   > Para saber mais sobre a criação de perfil leve, confira [Infraestrutura de criação de perfil de consulta](../../relational-databases/performance/query-profiling-infrastructure.md).
 
A lista de todos os nomes de USE HINT compatíveis pode ser consultada usando a exibição de gerenciamento dinâmico [sys.dm_exec_valid_use_hints](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md).    

> [!TIP]
> Os nomes de dica diferenciam maiúsculas de minúsculas.   
  
> [!IMPORTANT] 
> Algumas dicas USE HINT podem entrar em conflito com os sinalizadores de rastreamento habilitados no nível global ou no nível da sessão, ou com as definições de configurações de escopo do banco de dados. Nesse caso, a dica no nível da consulta (USE HINT) sempre terá precedência. Se um USE HINT estiver em conflito com outra dica de consulta ou com um sinalizador de rastreamento habilitado no nível da consulta (como por QUERYTRACEON), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um erro ao tentar executar a consulta. 

 USE PLAN N **'** _xml\_plan_ **'**      
 Força o otimizador de consulta a usar um plano de consulta existente para uma consulta especificada por **'** _xml\_plan_ **'** . USE PLAN não pode ser especificado com instruções INSERT, UPDATE, MERGE ou DELETE.  
  
TABLE HINT **(** _exposed\_object\_name_ [ **,** \<table_hint> [ [ **,** ]..._n_ ] ] **)** Aplica a dica de tabela especificada à tabela ou à exibição que corresponde ao _exposed\_object\_name_. É recomendável usar uma dica de tabela como uma dica de consulta apenas no contexto de um [guia de plano](../../relational-databases/performance/plan-guides.md).  
  
 _exposed\_object\_name_ pode ser uma das seguintes referências:  
  
-   Quando um alias é usado para a tabela ou exibição na cláusula [FROM](../../t-sql/queries/from-transact-sql.md) da consulta, _exposed\_object\_name_ é o alias.  
  
-   Quando um alias não é usado, _exposed\_object\_name_ é a correspondência exata da tabela ou exibição referenciada na cláusula FROM. Por exemplo, se a tabela ou exibição for referenciada usando um nome de duas partes, _exposed\_object\_name_ será esse mesmo nome de duas partes.  
  
 Quando você especifica _exposed\_object\_name_ sem especificar também uma dica de tabela, todos os índices especificados na consulta como parte de uma tabela para o objeto são desconsiderados. O otimizador de consulta, em seguida, determina o uso do índice. Você pode usar essa técnica para eliminar o efeito de uma dica de tabela INDEX quando não puder modificar a consulta original. Consulte o exemplo J.  
  
**\<table_hint> ::=** { [ NOEXPAND ] { INDEX ( _index\_value_ [ ,..._n_ ] ) | INDEX = ( _index\_value_ ) | FORCESEEK [ **(** _index\_value_ **(** _index\_column\_name_ [ **,** ... ] **))** ]| FORCESCAN | HOLDLOCK | NOLOCK | NOWAIT | PAGLOCK | READCOMMITTED | READCOMMITTEDLOCK | READPAST | READUNCOMMITTED | REPEATABLEREAD | ROWLOCK | SERIALIZABLE | SNAPSHOT | SPATIAL_WINDOW_MAX_CELLS | TABLOCK | TABLOCKX | UPDLOCK | XLOCK } É a dica de tabela a ser aplicada à tabela ou exibição que corresponde a *exposed_object_name* com uma dica de consulta. Para obter uma descrição dessas dicas, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Dicas de tabela diferentes de INDEX, FORCESCAN e FORCESEEK não são permitidas como dicas de consulta, a não ser que a consulta possua uma cláusula WITH que especifique a dica de tabela. Para obter mais informações, consulte Comentários.  
  
> [!CAUTION] 
> A especificação de FORCESEEK com parâmetros limita o número de planos que podem ser considerados pelo otimizador mais do que a especificação de FORCESEEK sem parâmetros. Isso pode resultar em um erro "Não é possível gerar o plano" em mais casos. Em uma versão futura, as modificações internas no otimizador talvez permitam a consideração de mais planos.  
  
## <a name="remarks"></a>Remarks  
 As dicas de consultas não podem ser especificadas em uma instrução INSERT, exceto quando uma cláusula SELECT é usada na instrução.  
  
 Só podem ser especificadas dicas de consulta na consulta de nível superior, e não em subconsultas. Quando uma dica de tabela é especificada como uma dica de consulta, a dica pode ser especificada na consulta de nível superior ou em uma subconsulta. No entanto, o valor especificado para _exposed\_object\_name_ na cláusula TABLE HINT deve corresponder exatamente ao nome exposto na consulta ou subconsulta.  
  
## <a name="specifying-table-hints-as-query-hints"></a>Especificando dicas de tabela como dicas de consulta  
 É recomendável usar a dica de tabela INDEX, FORCESCAN ou FORCESEEK como dica de consulta apenas no contexto de um [guia de plano](../../relational-databases/performance/plan-guides.md). Os guias de plano são úteis quando não é possível modificar a consulta original, por exemplo, por se tratar de um aplicativo de terceiros. A dica de consulta especificada na guia de plano é adicionada à consulta antes de ela ser compilada e otimizada. Para consultas ad hoc, use a cláusula TABLE HINT apenas ao testar instruções de guia de plano. Para todas as demais consultas ad hoc, é recomendável especificar essas dicas apenas como dicas de tabela.  
  
 Quando especificadas como uma dica de consulta, as dicas de tabela INDEX, FORCESCAN e FORCESEEK são válidas para os objetos a seguir:  
  
-   Tabelas  
-   Exibições  
-   Exibições indexadas  
-   Expressões de tabela comuns (a dica deve ser especificada na instrução SELECT cujo conjunto de resultados popula a expressão de tabela comum)  
-   Exibições de gerenciamento dinâmico  
-   Subconsultas nomeadas  
  
Você pode especificar as dicas de tabela INDEX, FORCESCAN e FORCESEEK como dicas de consulta para uma consulta que não tenha dicas de tabela. Você também pode usá-las para substituir as dicas existente INDEX, FORCESCAN ou FORCESEEK na consulta, respectivamente. 

Dicas de tabela diferentes de INDEX, FORCESCAN e FORCESEEK não são permitidas como dicas de consulta, a não ser que a consulta possua uma cláusula WITH que especifique a dica de tabela. Nesse caso, uma dica correspondente também deve ser especificada como uma dica de consulta. Especifique a dica correspondente como uma dica de consulta usando TABLE HINT na cláusula OPTION. Essa especificação preserva a semântica da consulta. Por exemplo, se a consulta contiver a dica de tabela NOLOCK, a cláusula OPTION no parâmetro **@hints** do guia de plano também precisará conter a dica NOLOCK. Consulte o exemplo K. 

O Erro 8072 ocorre em alguns cenários. Um deles é quando você especifica uma dica de tabela diferente de INDEX, FORCESCAN ou FORCESEEK usando TABLE HINT na cláusula OPTION sem uma dica de consulta correspondente. O segundo cenário é o oposto. Esse erro indica que a cláusula OPTION pode modificar a semântica da consulta, e a consulta falhará.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-merge-join"></a>A. Usando MERGE JOIN  
 O exemplo a seguir especifica que MERGE JOIN executa a operação JOIN na consulta. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
SELECT *   
FROM Sales.Customer AS c  
INNER JOIN Sales.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID  
WHERE TerritoryID = 5  
OPTION (MERGE JOIN);  
GO    
```  
  
### <a name="b-using-optimize-for"></a>B. Usando OPTIMIZE FOR  
 O exemplo a seguir instrui o otimizador de consulta a usar o valor `'Seattle'` para a variável local `@city_name` e a usar dados estatísticos para determinar o valor da variável local `@postal_code` ao otimizar a consulta. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
DECLARE @city_name nvarchar(30);  
DECLARE @postal_code nvarchar(15);  
SET @city_name = 'Ascheim';  
SET @postal_code = 86171;  
SELECT * FROM Person.Address  
WHERE City = @city_name AND PostalCode = @postal_code  
OPTION ( OPTIMIZE FOR (@city_name = 'Seattle', @postal_code UNKNOWN) );  
GO  
```  
  
### <a name="c-using-maxrecursion"></a>C. Usando MAXRECURSION  
 MAXRECURSION pode ser usado para impedir que uma expressão de tabela comum recursiva malformada entre em loop infinito. O exemplo a seguir cria um loop infinito intencionalmente e usa a dica MAXRECURSION para limitar o número de níveis de recursão para dois. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
--Creates an infinite loop  
WITH cte (CustomerID, PersonID, StoreID) AS  
(  
    SELECT CustomerID, PersonID, StoreID  
    FROM Sales.Customer  
    WHERE PersonID IS NOT NULL  
  UNION ALL  
    SELECT cte.CustomerID, cte.PersonID, cte.StoreID  
    FROM cte   
    JOIN  Sales.Customer AS e   
        ON cte.PersonID = e.CustomerID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT CustomerID, PersonID, StoreID  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 Depois que o erro de codificação for corrigido, MAXRECURSION não será mais necessário.  
  
### <a name="d-using-merge-union"></a>D. Usando MERGE UNION  
 O exemplo a seguir usa a dica de consulta MERGE UNION. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
SELECT *  
FROM HumanResources.Employee AS e1  
UNION  
SELECT *  
FROM HumanResources.Employee AS e2  
OPTION (MERGE UNION);  
GO  
```  
  
### <a name="e-using-hash-group-and-fast"></a>E. Usando HASH GROUP e FAST  
 O exemplo a seguir usa as dicas de consulta HASH GROUP e FAST. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO    
```  
  
### <a name="f-using-maxdop"></a>F. Usando MAXDOP  
 O exemplo a seguir usa a dica de consulta MAXDOP. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (MAXDOP 2);    
GO
```  
  
### <a name="g-using-index"></a>G. Usando INDEX  
 O exemplo a seguir usa a dica INDEX. O primeiro exemplo especifica um único índice. O segundo exemplo especifica vários índices para uma única referência de tabela. Em ambos os exemplos, como você aplica a dica INDEX em uma tabela que usa um alias, a cláusula TABLE HINT também deve especificar o mesmo alias do nome do objeto exposto. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX (IX_Employee_ManagerID)))';  
GO  
EXEC sp_create_plan_guide   
    @name = N'Guide2',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX(PK_Employee_EmployeeID, IX_Employee_ManagerID)))';  
GO    
```  
  
### <a name="h-using-forceseek"></a>H. Usando FORCESEEK  
 O exemplo a seguir usa a dica de tabela FORCESEEK. A cláusula TABLE HINT também deve especificar o mesmo nome de duas partes que o nome do objeto exposto. Especifique o nome ao aplicar a dica INDEX em uma tabela que usa um nome de duas partes. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide3',   
    @stmt = N'SELECT c.LastName, c.FirstName, HumanResources.Employee.Title  
              FROM HumanResources.Employee  
              JOIN Person.Contact AS c ON HumanResources.Employee.ContactID = c.ContactID  
              WHERE HumanResources.Employee.ManagerID = 3  
              ORDER BY c.LastName, c.FirstName;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT( HumanResources.Employee, FORCESEEK))';  
GO    
```  
  
### <a name="i-using-multiple-table-hints"></a>I. Usando várias dicas de tabela  
 O exemplo a seguir aplica a dica INDEX a uma tabela e a dica FORCESEEK a outra. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide4',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX( IX_Employee_ManagerID))   
                       , TABLE HINT (c, FORCESEEK))';  
GO  
```  
  
### <a name="j-using-table-hint-to-override-an-existing-table-hint"></a>J. Usando TABLE HINT para substituir uma dica de tabela existente  
O exemplo a seguir mostra como usar a dica TABLE HINT. É possível usar a dica sem especificar uma dica para substituir o comportamento da dica de tabela INDEX que você especifica na cláusula FROM da consulta. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide5',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e WITH (INDEX (IX_Employee_ManagerID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e))';  
GO    
```  
  
### <a name="k-specifying-semantics-affecting-table-hints"></a>K. Especificando dicas de tabela que afetam a semântica  
O exemplo a seguir contém duas dicas de tabela na consulta: NOLOCK, que afeta a semântica, e INDEX, que não afeta a semântica. Para preservar a semântica da consulta, a dica NOLOCK é especificada na cláusula OPTIONS do guia de plano. Em conjunto com a dica NOLOCK, especifique as dicas INDEX e FORCESEEK e substitua a dica INDEX, que não afeta a semântica, na consulta durante a compilação e otimização da instrução. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide6',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX(IX_Employee_ManagerID), NOLOCK, FORCESEEK))';  
GO    
```  
  
O exemplo a seguir mostra um método alternativo para preservar a semântica da consulta e permitir que o otimizador escolha um índice diferente do índice especificado na dica de tabela. Permita que o otimizador escolha especificando a dica NOLOCK na cláusula OPTIONS. Você especifica a dica porque ela afeta a semântica. Em seguida, especifica a palavra-chave TABLE HINT com apenas uma referência de tabela e nenhuma dica INDEX. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide7',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, NOLOCK))';  
GO  
```  
### <a name="l-using-use-hint"></a>L. Usando USE HINT  
 O exemplo a seguir usa as dicas de consulta RECOMPILE e USE HINT. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```sql  
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (RECOMPILE, USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES', 'DISABLE_PARAMETER_SNIFFING')); 
GO  
```  
    
## <a name="see-also"></a>Consulte Também  
[Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
[sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
[sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
[Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)       
[Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)      
  
