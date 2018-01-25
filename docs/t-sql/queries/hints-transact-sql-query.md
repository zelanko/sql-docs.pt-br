---
title: Consulta de dicas (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
dev_langs: TSQL
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
ms.assetid: 66fb1520-dcdf-4aab-9ff1-7de8f79e5b2d
caps.latest.revision: "136"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0a3c74aa7b1da86c6d0ac54025d337700019465d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="hints-transact-sql---query"></a>Dicas (Transact-SQL) - consulta
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  As dicas de consulta especificam que as dicas indicadas devem ser usadas em toda a consulta. Elas afetam todos os operadores na instrução. Se UNION estiver envolvida na consulta principal, só a última consulta envolvendo uma operação UNION poderá ter a cláusula OPTION. Dicas de consulta são especificadas como parte do [cláusula OPTION](../../t-sql/queries/option-clause-transact-sql.md). Se uma ou mais dicas de consulta fizerem com que o otimizador de consulta não gere um plano válido, será emitido o erro 8622.  
  
> [!CAUTION]  
>  Como o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleciona, normalmente, o melhor plano de execução para uma consulta, recomendamos usar dicas apenas como último recurso para desenvolvedores e administradores de banco de dados experientes.  
  
 **Aplica-se a:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 Especifica que as agregações descritas na cláusula GROUP BY ou DISTINCT da consulta devem usar hash ou ordenação.  
  
 { MERGE | HASH | CONCAT } UNION  
 Especifica que todas as operações UNION são executadas por mesclagem, hash ou concatenação de conjuntos de UNION. Se mais de uma dica de UNION for especificada, o otimizador de consulta selecionará a estratégia menos cara dentre as dicas especificadas.  
  
 { LOOP | MERGE | HASH } JOIN  
 Especifica que todas as operações de junção são executadas por LOOP JOIN, MERGE JOIN ou HASH JOIN na consulta inteira. Se mais de uma dica de junção for especificada, o otimizador selecionará a estratégia de junção menos cara dentre as permitidas.  
  
 Se, na mesma consulta, uma dica de junção for especificada também na cláusula FROM para um par de tabelas específico, essa dica de junção terá precedência na junção das duas tabelas, embora as dicas de consulta ainda devam ser consideradas. Portanto, a dica de junção para o par de tabelas pode restringir apenas a seleção de métodos de junção permitidos na dica de consulta. Para obter mais informações, consulte [dicas de junção &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-join.md).  
  
 EXPAND VIEWS  
 Especifica que as exibições indexadas são expandidas e o otimizador de consulta não considerará nenhuma exibição indexada como uma substituta de qualquer parte da consulta. Uma exibição é expandida quando o nome da exibição é substituído por sua definição no texto da consulta.  
  
 Esta dica de consulta desabilita o uso direto de exibições indexadas e índices em exibições indexadas no plano de consulta.  
  
 A exibição indexada não será expandida apenas se a exibição receber referência direta na parte SELECT da consulta e WITH (NOEXPAND) ou WITH (NOEXPAND, INDEX ( *index_value* [**, *... n* ])) é especificado. Para obter mais informações sobre a dica de consulta WITH (NOEXPAND), consulte [FROM](../../t-sql/queries/from-transact-sql.md).  
  
 Apenas as exibições na parte SELECT das instruções, inclusive aquelas nas instruções INSERT, UPDATE, MERGE e DELETE são afetadas pela dica.  
  
 FAST *number_rows*  
 Especifica que a consulta é otimizada para recuperação rápida dos primeiros *number_rows.* Este é um inteiro não negativo. Após a primeira *number_rows* são retornados, a consulta continua a execução e produz seu conjunto de resultados completo.  
  
 FORCE ORDER  
 Especifica que a ordem de junção indicada pela sintaxe de consulta é preservada durante a otimização da consulta. Usar FORCE ORDER não afeta o possível comportamento de reversão de função do otimizador de consulta.  
  
> [!NOTE]  
>  Em uma instrução MERGE, a tabela de origem é acessada antes da tabela de destino como a ordem de junção padrão, a menos que a cláusula WHEN SOURCE NOT MATCHED seja especificada. Especificar FORCE ORDER preserva esse comportamento padrão.  
  
 {FORCE | DESABILITAR} EXTERNALPUSHDOWN  
 Forçar ou desabilite o empilhamento de cálculo de qualificação expressões no Hadoop. Só se aplica a consultas usando PolyBase. Não enviará para o armazenamento do Azure.  
  
 KEEP PLAN  
 Força o otimizador de consulta a relaxar o limite de recompilação estimado para uma consulta. O limite de recompilação estimado é o ponto no qual uma consulta é recompilada automaticamente quando o número calculado de alterações de colunas indexadas tiver sido efetuado em uma tabela por meio da execução da instrução UPDATE, DELETE, MERGE ou INSERT. Especificar KEEP PLAN assegura que uma consulta não seja recompilada tão frequentemente como quando há várias atualizações em uma tabela.  
  
 KEEPFIXED PLAN  
 Força o otimizador de consulta a não recompilar uma consulta devido a alterações nas estatísticas. Especificar KEEPFIXED PLAN assegura que uma consulta seja recompilada apenas se o esquema das tabelas subjacentes for alterado ou se **sp_recompile** é executado em relação a essas tabelas.  
  
 IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Impede que a consulta usando um índice de columnstore otimizado de memória não clusterizado. Se a consulta contiver a dica de consulta para evitar o uso do índice columnstore e uma dica de índice para usar um índice columnstore, as dicas entrarão em conflito e a consulta retornará um erro.  
  
 MAX_GRANT_PERCENT = *percent*  
 O máximo de memória concedida tamanho em porcentagem. A consulta é garantida para não exceder esse limite. O limite real pode ser menor se o administrador de recursos definindo é menor do que isso. Os valores válidos são entre 0.0 e 100.0.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 MIN_GRANT_PERCENT = *percent*  
 Tamanho em porcentagem de conceder o mínimo de memória = % de limite padrão. A consulta é garantida para obter o máximo (memória necessária, grant min) porque necessário pelo menos a memória é necessária para iniciar uma consulta. Os valores válidos são entre 0.0 e 100.0.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 MAXDOP *number*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Substitui o **grau máximo de paralelismo** opção de configuração de **sp_configure** e administrador de recursos para a consulta especificar essa opção. A dica de consulta MAXDOP pode exceder o valor configurado com sp_configure. Se MAXDOP exceder o valor configurado com o administrador de recursos, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa o valor de MAXDOP Resource Governor, descrito em [ALTER WORKLOAD GROUP &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-workload-group-transact-sql.md). Todas as regras semânticas usadas com o **grau máximo de paralelismo** opção de configuração são aplicáveis quando você usar a dica de consulta MAXDOP. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
  
> [!WARNING]  
> Se MAXDOP estiver definido como 0, o servidor escolherá o max degree of parallelism.  
  
 MAXRECURSION *número*  
 Especifica o número máximo de recursões permitidas para esta consulta. *número* é um inteiro não negativo entre 0 e 32767. Quando 0 é especificado, nenhum limite é aplicado. Se essa opção não for especificada, o limite padrão para o servidor será de 100.  
  
 Quando o número especificado ou padrão de limite de MAXRECURSION é atingido durante a execução da consulta, a consulta é encerrada e um erro é retornado.  
  
 Por causa desse erro, todos os efeitos da instrução são revertidos. Se a instrução for do tipo SELECT, poderão ser retornados resultados parciais ou nenhum resultado. Eventuais resultados parciais retornados podem não incluir todas as linhas em níveis de recursão acima do nível de recursão máximo especificado.  
  
 Para obter mais informações, consulte [com common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 NO_PERFORMANCE_SPOOL  
 **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Impede que um operador de spool seja adicionado a planos de consulta (exceto os planos quando spool é necessária para garantir a semântica de atualização válido). Em alguns cenários, o operador de spool pode reduzir o desempenho. Por exemplo, o spool usa tempdb e contenção de tempdb pode ocorrer se um há várias consultas simultâneas em execução com as operações de spool.  
  
 OPTIMIZE FOR (  *@variable_name*  {desconhecido | = *literal_constant}* [ **,** ... *n* ] )  
 Instrui o otimizador de consulta a usar um valor específico para uma variável local quando a consulta é compilada e otimizada. O valor é usado somente durante a otimização da consulta e não durante sua execução.  
  
 *@variable_name*  
 É o nome de uma variável local usada em uma consulta para a qual um valor pode ser atribuído para uso com a dica de consulta OPTIMIZE FOR.  
  
 *DESCONHECIDO*  
 Especifica que o otimizador de consulta usa dados estatísticos e não o valor inicial para determinar o valor de uma variável local durante a otimização da consulta.  
  
 *literal_constant*  
 É um valor literal constante a ser atribuído  *@variable_name*  para uso com a dica de consulta OPTIMIZE FOR. *literal_constant* é usado somente durante a otimização de consulta e não como o valor de  *@variable_name*  durante a execução da consulta. *literal_constant* pode ser de qualquer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados do sistema que pode ser expresso como uma constante literal. O tipo de dados *literal_constant* deve ser implicitamente conversível em dados tipo  *@variable_name*  referências na consulta.  
  
 OPTIMIZE FOR pode anular o comportamento de detecção de parâmetro padrão do otimizador ou pode ser usado na criação de guias de plano. Para obter mais informações, consulte [recompilar um procedimento armazenado](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md).  
  
 OPTIMIZE FOR UNKNOWN  
 Instrui o otimizador de consulta a usar dados estatísticos e não os valores iniciais para todas as variáveis locais quando a consulta é compilada e otimizada, incluindo parâmetros criados com parametrização forçada.  
  
 Se OPTIMIZE FOR @variable_name = *literal_constant* e OPTIMIZE FOR UNKNOWN forem usados na mesma dica de consulta, o otimizador de consulta usará o *literal_constant* que é especificado para um valor específico e DESCONHECIDO para os valores das variáveis restantes. Os valores só são usados durante a otimização de consulta e não durante a execução das consultas.  
  
 PARAMETERIZATION { SIMPLE | FORCED }  
 Especifica as regras de parametrização que o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica à consulta quando ela é compilada.  
  
> [!IMPORTANT]  
> A dica de consulta PARAMETERIZATION só pode ser especificada dentro de um guia de plano. Ela não pode ser especificada diretamente dentro de uma consulta.  
  
 SIMPLE instrui o otimizador de consulta a tentar parametrização simples. FORCED instrui o otimizador de consulta a tentar parametrização forçada. A dica de consulta PARAMETERIZATION é usada para substituir a configuração atual da opção SET do banco de dados PARAMETERIZATION dentro de um guia de plano. Para obter mais informações, consulte [especificar comportamento de parametrização de consulta por guias de plano usando](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md).  
  
 RECOMPILE  
 Instrui o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] a descartar o plano gerado para a consulta depois de sua execução, forçando o otimizador de consulta a recompilar um plano de consulta da próxima vez que a mesma consulta for executada. Sem especificar RECOMPILE, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena em cache os planos de consulta e os reutiliza. Ao compilar planos de consulta, a dica de consulta RECOMPILE usa os valores atuais de todas as variáveis locais na consulta e, se a consulta estiver dentro de um procedimento armazenado, os valores atuais serão passados para quaisquer parâmetros.  
  
 RECOMPILE é uma alternativa útil à criação de um procedimento armazenado que utiliza a cláusula WITH RECOMPILE quando só um subconjunto de consultas dentro do procedimento armazenado, em vez de todo o procedimento armazenado, deve ser recompilado. Para obter mais informações, consulte [recompilar um procedimento armazenado](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md). RECOMPILE também é útil para a criação de guias de plano.  
  
 ROBUST PLAN  
 Força o otimizador de consulta a tentar um plano que trabalhe para o tamanho máximo de linhas potenciais, possivelmente às custas do desempenho. Quando a consulta é processada, tabelas e operadores intermediários podem precisar armazenar e processar linhas maiores do que qualquer uma das linhas de entrada. As linhas podem ser tão grandes que, às vezes, o operador particular não consegue processá-las. Se isso ocorrer, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] produzirá um erro durante a execução da consulta. Usando ROBUST PLAN, você instrui o otimizador de consulta a não considerar nenhum plano de consulta que possa encontrar esse problema.  
  
 Se tal plano não for possível, o otimizador de consulta retornará um erro, em vez de adiar a detecção de erros para a execução da consulta. Linhas podem conter colunas de tamanho variável. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] permite definir linhas com o tamanho potencial máximo para além da capacidade de processamento do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Geralmente, apesar do tamanho potencial máximo, um aplicativo armazena linhas cujos tamanhos reais estão dentro dos limites de processamento do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] encontrar uma linha longa demais, será retornado um erro de execução.  
 
<a name="use_hint"></a>Dica de uso ( **'***hint_name***'** )  
 **Aplica-se a**: aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) e [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
 
 Fornece uma ou mais dicas adicionais para o processador de consulta conforme especificado por um nome de dica **dentro de aspas simples**. 

 Há suporte para os seguintes nomes de dica:
 
*  'DISABLE_OPTIMIZED_NESTED_LOOP'  
 Instrui o processador de consultas para não usar uma operação de classificação (Classificar em lotes) para junções de loops aninhados otimizado ao gerar um plano de consulta. Isso é equivalente a [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2340.
*  'FORCE_LEGACY_CARDINALITY_ESTIMATION'  
 Força o otimizador de consulta para usar [estimativa de cardinalidade](../../relational-databases/performance/cardinality-estimation-sql-server.md) modelo de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões anteriores. Isso é equivalente a [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481 ou [Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) configuração LEGACY_CARDINALITY_ESTIMATION = ON.
*  'ENABLE_QUERY_OPTIMIZER_HOTFIXES'  
 Habilita hotfixes Otimizador de consulta (alterações lançadas em atualizações cumulativas do SQL Server e Service Packs). Isso é equivalente a [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4199 ou [Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) definindo QUERY_OPTIMIZER_HOTFIXES = ON.
*  'DISABLE_PARAMETER_SNIFFING'  
 Instrui o otimizador de consulta para usar a distribuição de média de dados durante a compilação de uma consulta com um ou mais parâmetros, fazendo com que o plano de consulta independente no valor de parâmetro que foi usado primeiro quando a consulta foi compilada. Isso é equivalente a [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4136 ou [Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) definindo PARAMETER_SNIFFING = OFF.
*  'ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES'  
 Faz com que o SQL Server gerar um plano usando seletividade mínimo ao estimar predicados e filtros de levar em conta a correlação. Isso é equivalente a [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4137 quando usado com o modelo de estimativa de cardinalidade de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões anteriores, e tem efeito similar ao [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9471 é usado com cardinalidade modelo de estimativa de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou superior.
*  'DISABLE_OPTIMIZER_ROWGOAL'  
 Faz com que o SQL Server gerar um plano que não usa os ajustes de meta de linha com consultas que contenham TOP, OPTION (FAST N), ou existe palavras-chave. Isso é equivalente a [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4138.
*  'ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS'  
 Habilita as estatísticas geradas automaticamente rápidas (alteração de histograma) para qualquer coluna de índice à esquerda para a qual cardinalidade estimativa é necessário. O histograma usado para estimativa de cardinalidade será ajustado em tempo de compilação de consulta para a conta para o valor máximo ou mínimo real dessa coluna. Isso é equivalente a [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4139. 
*  'ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS'  
 Faz com que o SQL Server gerar um plano de consulta usando a suposição de confinamento simples em vez da suposição de contenção de Base padrão para junções, sob o otimizador de consulta [estimativa de cardinalidade](../../relational-databases/performance/cardinality-estimation-sql-server.md) modelo de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou mais recente. Isso é equivalente a [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9476. 
*  'FORCE_DEFAULT_CARDINALITY_ESTIMATION'  
 Força o otimizador de consulta para usar [estimativa de cardinalidade](../../relational-databases/performance/cardinality-estimation-sql-server.md) modelo que corresponde ao nível de compatibilidade de banco de dados atual. Use essa dica para substituir [Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) configuração LEGACY_CARDINALITY_ESTIMATION = ON ou [sinalizador de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481.
 
> [!TIP]
> Nomes de dica diferenciam maiusculas de minúsculas.
  
  A lista de todos os nomes de dica de USE com suporte pode ser consultada usando a exibição de gerenciamento dinâmico [sys.dm_exec_valid_use_hints ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md).
> [!IMPORTANT] 
> Algumas dicas de dica de USE podem entrar em conflito com os sinalizadores de rastreamento habilitados no nível global ou configurações de escopo de nível de sessão ou o banco de dados. Nesse caso, a dica de nível de consulta (dica USE) sempre terá precedência. Se uma dica USE está em conflito com outra dica de consulta ou um sinalizador de rastreamento habilitado no nível da consulta (como por QUERYTRACEON), SQL Server irá gerar um erro ao tentar executar a consulta. 

 USE PLAN N**'***xml_plan***'**  
 Força o otimizador de consulta para usar um plano de consulta existente para uma consulta que é especificada pelo **'***xml_plan***'**. USE PLAN não pode ser especificado com instruções INSERT, UPDATE, MERGE ou DELETE.  
  
Dica de tabela  **(* exposed_object_name* [ **,** \<table_hint > [[* *,**]...  *n*  ]] **)** Aplica-se a dica de tabela especificada para a tabela ou exibição que corresponde ao *exposed_object_name*. É recomendável usar uma dica de tabela como uma dica de consulta apenas no contexto de um [guia de plano](../../relational-databases/performance/plan-guides.md).  
  
 *exposed_object_name* pode ser uma das seguintes referências:  
  
-   Quando um alias é usado para a tabela ou exibição no [FROM](../../t-sql/queries/from-transact-sql.md) cláusula da consulta, *exposed_object_name* é o alias.  
  
-   Quando um alias não for usado, *exposed_object_name* a correspondência exata da tabela ou exibição referenciada na cláusula FROM. Por exemplo, se a tabela ou exibição é referenciada usando um nome de duas partes, *exposed_object_name* é o mesmo nome de duas partes.  
  
 Quando *exposed_object_name* é especificado sem especificar uma dica de tabela, quaisquer índices especificados na consulta como parte de uma dica de tabela para o objeto é desconsiderado e o uso de índice é determinado pelo otimizador de consulta. Você pode usar essa técnica para eliminar o efeito de uma dica de tabela INDEX quando não puder modificar a consulta original. Consulte o exemplo J.  
  
**\<table_hint >:: =** {[NOEXPAND] {índice ( *index_value* [,... *n* ] ) | ÍNDICE = ( *index_value* ) | FORCESEEK [**(***index_value***(* index_column_name* [**,**...] **))** ]| FORCESCAN | HOLDLOCK | NOLOCK | NOWAIT | PAGLOCK | READCOMMITTED | READCOMMITTEDLOCK | READPAST | READUNCOMMITTED | REPEATABLEREAD | ROWLOCK | SERIALIZÁVEL | INSTANTÂNEO | SPATIAL_WINDOW_MAX_CELLS | TABLOCK | TABLOCKX | UPDLOCK | XLOCK} é a dica de tabela para aplicar à tabela ou exibição que corresponde ao *exposed_object_name* como uma dica de consulta. Para obter uma descrição dessas dicas, consulte [dicas de tabela &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Dicas de tabela diferentes de INDEX, FORCESCAN e FORCESEEK não são permitidas como dicas de consulta, a não ser que a consulta possua uma cláusula WITH que especifique a dica de tabela. Para obter mais informações, consulte Comentários.  
  
> [!CAUTION] 
> A especificação de FORCESEEK com parâmetros limita o número de planos que podem ser considerados pelo otimizador mais do que a especificação de FORCESEEK sem parâmetros. Isso pode resultar em um erro "Não é possível gerar o plano" em mais casos. Em uma versão futura, as modificações internas no otimizador talvez permitam a consideração de mais planos.  
  
## <a name="remarks"></a>Remarks  
 Não podem ser especificadas dicas de consulta em uma instrução INSERT, exceto quando uma cláusula SELECT for usada dentro da instrução.  
  
 Só podem ser especificadas dicas de consulta na consulta de nível superior, e não em subconsultas. Quando uma dica de tabela é especificada como uma dica de consulta, a dica pode ser especificada na consulta de nível superior ou em uma subconsulta; No entanto, o valor especificado para *exposed_object_name* na dica de tabela cláusula deve corresponder exatamente ao nome exposto na consulta ou subconsulta.  
  
## <a name="specifying-table-hints-as-query-hints"></a>Especificando dicas de tabela como dicas de consulta  
 É recomendável usar a dica de tabela INDEX, FORCESCAN ou FORCESEEK como dica de consulta apenas no contexto de um [guia de plano](../../relational-databases/performance/plan-guides.md). Guias de plano são úteis quando não é possível modificar a consulta original, por exemplo, por se tratar de um aplicativo de terceiros. A dica de consulta especificada na guia de plano é adicionada à consulta antes de ela ser compilada e otimizada. Para consultas ad hoc, use a cláusula TABLE HINT apenas ao testar instruções de guia de plano. Para todas as demais consultas ad hoc, é recomendável especificar essas dicas apenas como dicas de tabela.  
  
 Quando especificadas como uma dica de consulta, as dicas de tabela INDEX, FORCESCAN e FORCESEEK são válidas para os objetos a seguir:  
  
-   Tabelas  
  
-   Exibições  
  
-   Exibições indexadas  
  
-   Expressões de tabela comuns (a dica deve ser especificada na instrução SELECT cujo conjunto de resultados popula a expressão de tabela comum)  
  
-   Exibições de gerenciamento dinâmico  
  
-   Subconsultas nomeadas  
  
 As dicas de tabela INDEX, FORCESCAN e FORCESEEK podem ser especificadas como dicas de consulta para uma consulta que não tem dicas de tabela existentes ou podem ser usadas para substituir dicas INDEX, FORCESCAN ou FORCESEEK existentes na consulta, respectivamente. Dicas de tabela diferentes de INDEX, FORCESCAN e FORCESEEK não são permitidas como dicas de consulta, a não ser que a consulta possua uma cláusula WITH que especifique a dica de tabela. Nesse caso, será necessário especificar também uma dica correspondente como dica de consulta usando TABLE HIT na cláusula OPTION para preservar a semântica da consulta. Por exemplo, se a consulta contiver a dica de tabela NOLOCK, a cláusula OPTION no  **@hints**  parâmetro do guia de plano também deverá conter a dica NOLOCK. Consulte o exemplo K. Quando uma dica de tabela diferente de INDEX, FORCESCAN ou FORCESEEK é especificada usando a dica de tabela na cláusula OPTION sem uma dica de consulta correspondente, ou vice-versa; Erro 8702 é gerado (indicando que a cláusula OPTION pode fazer com que a semântica da consulta) e a consulta falha.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-merge-join"></a>A. Usando MERGE JOIN  
 O exemplo a seguir especifica que a operação de junção na consulta é executada por junção de mesclagem. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
SELECT *   
FROM Sales.Customer AS c  
INNER JOIN Sales.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID  
WHERE TerritoryID = 5  
OPTION (MERGE JOIN);  
GO    
```  
  
### <a name="b-using-optimize-for"></a>B. Usando OPTIMIZE FOR  
 O exemplo a seguir instrui o otimizador de consulta para usar o valor `'Seattle'` para variável local `@city_name` e usar dados estatísticos para determinar o valor da variável local `@postal_code` ao otimizar a consulta. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
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
 MAXRECURSION pode ser usado para impedir que uma expressão de tabela comum recursiva malformada entre em loop infinito. Intencionalmente, o exemplo a seguir cria um loop infinito e usa a dica MAXRECURSION para limitar o número de níveis de recursão a dois. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
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
 O exemplo a seguir usa a dica de consulta de união de mesclagem. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
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
  
```  
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
  
```  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (MAXDOP 2);    
GO
```  
  
### <a name="g-using-index"></a>G. Usando INDEX  
 O exemplo a seguir usa a dica INDEX. O primeiro exemplo especifica um único índice. O segundo exemplo especifica vários índices para uma única referência de tabela. Nos dois exemplos, uma vez que a dica INDEX é aplicada em uma tabela que usa um alias, a cláusula TABLE HINT também deve especificar o mesmo alias como nome do objeto exposto. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
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
 O exemplo a seguir usa a dica de tabela FORCESEEK. Como a dica INDEX é aplicada em uma tabela que usa um nome de duas partes, a cláusula TABLE HINT também deve especificar o mesmo nome de duas partes como nome do objeto exposto. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
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
  
```  
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
 O exemplo a seguir mostra como usar a dica TABLE HINT sem especificar uma dica para substituir o comportamento da dica de tabela INDEX especificada na cláusula FROM da consulta. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
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
 O exemplo a seguir contém duas dicas de tabela na consulta: NOLOCK, que afeta a semântica, e INDEX, que não afeta a semântica. Para preservar a semântica da consulta, a dica NOLOCK é especificada na cláusula OPTIONS do guia de plano. Além da dica NOLOCK, as dicas INDEX e FORCESEEK são especificadas e substituem a dica INDEX, que não afeta a semântica, na consulta, quando a instrução é compilada e otimizada. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
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
  
 O exemplo a seguir mostra um método alternativo para preservar a semântica da consulta e permitir que o otimizador escolha um índice diferente do índice especificado na dica de tabela. Isso é feito especificando-se a dica NOLOCK na cláusula OPTIONS (porque afeta a semântica) e a palavra-chave TABLE HINT com apenas uma referência de tabela e nenhuma dica INDEX. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
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
### <a name="l-using-use-hint"></a>L. Usando a dica USE  
 O exemplo a seguir usa as dicas de consulta RECOMPILE e dica de uso. O exemplo usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```  
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (RECOMPILE, USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES', 'DISABLE_PARAMETER_SNIFFING')); 
GO  
```  
    
## <a name="see-also"></a>Consulte também  
 [Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
 [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
