---
title: "Estatísticas | Microsoft Docs"
ms.custom: 
ms.date: 04/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-statistics
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statistical information [SQL Server], query optimization
- query performance [SQL Server], statistics
- query optimization statistics [SQL Server]
- statistical information [SQL Server], database options
- query optimization statistics [SQL Server], about query optimization statistics
- statistical information [SQL Server], guidelines
- statistical information [SQL Server]
- using statistics [SQL Server]
- statistical information [SQL Server], indexes
- index statistics [SQL Server]
- query optimizer [SQL Server], statistics
- statistics [SQL Server]
ms.assetid: b86a88ba-4f7c-4e19-9fbd-2f8bcd3be14a
caps.latest.revision: 70
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e098a8f837d216f18bb1310db3164b57f24575ba
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="statistics"></a>Estatísticas
  O otimizador de consulta utiliza estatísticas para criar planos de consulta que melhoram o desempenho das consultas. Para a maioria das consultas, o otimizador de consulta já gera as estatísticas necessárias para um plano de consulta de alta qualidade; em alguns casos, é necessário criar estatísticas adicionais ou modificar o design da consulta para obter melhores resultados. Este tópico aborda os conceitos de estatísticas e fornece diretrizes para o uso eficiente de estatísticas de otimização de consultas.  
  
##  <a name="DefinitionQOStatistics"></a> Componentes e conceitos  
 Estatísticas  
 As estatísticas de otimização de consulta são objetos que contêm informações estatísticas sobre a distribuição de valores em uma ou mais colunas de uma tabela ou exibição indexada. O otimizador de consulta usa essas estatísticas para estimar a *cardinalidade*, ou número de linhas, no resultado de consulta. Essas *estimativas de cardinalidade* permitem que o otimizador de consulta crie um plano de consulta de alta qualidade. Por exemplo, o otimizador de consulta pode usar estimativas de cardinalidade para escolher o operador index seek em vez do operador index scan, que utiliza mais recursos, e, assim, melhorar o desempenho das consultas.  
  
 Cada objeto de estatísticas é criado em uma lista de uma ou mais colunas de tabela e inclui um histograma que exibe a distribuição de valores na primeira coluna. Os objetos de estatísticas em várias colunas também armazenam informações estatísticas sobre a correlação de valores entre as colunas. Essas estatísticas de correlação, ou *densidades*, são derivadas do número de linhas distintas de valores de coluna. Para obter mais informações sobre objetos de estatísticas, veja [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).  
  
 Estatísticas filtradas  
 As estatísticas filtradas podem melhorar o desempenho de consultas selecionadas em subconjuntos bem definidos de dados. As estatísticas filtradas usam um predicado do filtro para selecionar o subconjunto de dados incluído nas estatísticas. Estatísticas filtradas bem projetadas podem aprimorar o plano de execução de consultas em comparação com as estatísticas de tabela completa. Para obter mais informações sobre o predicado de filtro, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md). Para obter mais informações sobre quando criar estatísticas filtradas, consulte a seção [Quando criar estatísticas](#UpdateStatistics) neste tópico. Para um estudo de caso, consulte a entrada de blog, [Usando estatísticas filtradas com tabelas particionadas](http://go.microsoft.com/fwlink/?LinkId=178505), no site do SQLCAT.  
  
 Opções de estatísticas  
 Há três opções que você pode definir que afetam quando e como as estatísticas são criadas e atualizadas. Estas opções são definidas no nível do banco de dados somente.  
  
 Opção AUTO_CREATE_STATISTICS  
 Quando a opção de criação automática de estatísticas, AUTO_CREATE_STATISTICS, está ativada, o otimizador de consulta cria estatísticas em colunas individuais no predicado de consulta, conforme necessário, a fim de melhorar as estimativas de cardinalidade do plano de consulta. Essas estatísticas de coluna única são criadas em colunas que ainda não têm um histograma em um objeto de estatísticas existente. A opção AUTO_CREATE_STATISTICS não determina se são criadas estatísticas para índices. Essa opção também não gera estatísticas filtradas. Ela se aplica estritamente a estatísticas de coluna única para a tabela completa.  
  
 Quando o otimizador de consulta cria estatísticas como resultado do uso da opção AUTO_CREATE_STATISTICS, os nomes das estatísticas iniciam com `_WA`. Você pode usar a consulta a seguir para determinar se o otimizador de consulta criou estatísticas para uma coluna de predicado de consulta.  
  
```  
SELECT OBJECT_NAME(s.object_id) AS object_name,  
    COL_NAME(sc.object_id, sc.column_id) AS column_name,  
    s.name AS statistics_name  
FROM sys.stats AS s JOIN sys.stats_columns AS sc  
    ON s.stats_id = sc.stats_id AND s.object_id = sc.object_id  
WHERE s.name like '_WA%'  
ORDER BY s.name;  
```  
  
 Opção AUTO_UPDATE_STATISTICS  
 Quando a opção de atualização automática de estatísticas, AUTO_UPDATE_STATISTICS, está ativada, o otimizador de consulta determina quando as estatísticas podem estar desatualizadas e as atualiza quando são usadas por uma consulta. As estatísticas ficam desatualizadas depois que operações de inserção, atualização, exclusão ou mesclagem alteram a distribuição de dados na tabela ou na exibição indexada. O otimizador de consulta determina quando estatísticas podem estar desatualizadas contando o número de modificações de dados desde a última atualização das estatísticas e comparando o número de modificações a um limite. O limite se baseia no número de linhas na tabela ou na exibição indexada.  
  
-   O SQL Server (2014 e anteriores) usa um limite com base na porcentagem de linhas alteradas. Isso ocorre independentemente do número de linhas na tabela.  
  
-   O SQL Server (a partir do 2016 e no nível de compatibilidade 130) usa um limite ajustado de acordo com o número de linhas na tabela. Com essa alteração, as estatísticas em tabelas grandes serão atualizadas com mais frequência.  
  
 O otimizador de consulta procura estatísticas desatualizadas antes de compilar uma consulta e antes de executar um plano de consulta em cache. Antes de compilar uma consulta, o otimizador de consulta usa as colunas, tabelas e exibições indexadas no predicado de consulta para determinar quais estatísticas podem estar desatualizadas. Antes de executar um plano de consulta em cache, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se o plano de consulta faz referência a estatísticas atualizadas.  
  
 A opção AUTO_UPDATE_STATISTICS se aplica a objetos de estatísticas criados para índices, colunas únicas em predicados de consulta e estatísticas criadas com a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) . Essa opção também se aplica a estatísticas filtradas.  
  
 AUTO_UPDATE_STATISTICS_ASYNC  
 A opção de atualização de estatísticas assíncrona, AUTO_UPDATE_STATISTICS_ASYNC, determina se o otimizador de consulta usa atualizações de estatísticas síncronas ou assíncronas. Por padrão, a opção de atualização de estatísticas assíncrona está desativada e o otimizador de consulta atualiza estatísticas de forma síncrona. A opção AUTO_UPDATE_STATISTICS_ASYNC se aplica a objetos de estatísticas criados para índices, colunas únicas em predicados de consulta e estatísticas criadas com a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) .  
  
 As atualizações de estatísticas podem ser síncronas (o padrão) ou assíncronas. Com as atualizações de estatísticas síncronas, as consultas são sempre compiladas e executadas com estatísticas atualizadas. Quando as estatísticas estão desatualizadas, o otimizador de consulta aguarda estatísticas atualizadas antes de compilar e executar a consulta. Com as atualizações de estatísticas assíncronas, as consultas são compiladas com estatísticas existentes, mesmo que elas estejam desatualizas. O otimizador de consulta poderá escolher um plano de consulta com qualidade inferior se as estatísticas estiverem desatualizadas na compilação da consulta. As consultas compiladas após a conclusão das atualizações assíncronas serão beneficiadas por usarem estatísticas atualizadas.  
  
 Considere o uso de estatísticas síncronas ao executar operações que alteram a distribuição de dados, como truncar uma tabela ou executar uma atualização em massa de uma porcentagem grande das linhas. Se você não atualizar as estatísticas depois de concluir a operação, o uso de estatísticas síncronas garantirá que as estatísticas sejam atualizadas antes de executar consultas nos dados alterados.  
  
 Considere o uso de estatísticas assíncronas para obter tempos de resposta de consulta mais previsíveis para os seguintes cenários:  
  
-   Seu aplicativo executa frequentemente a mesma consulta, consultas semelhantes ou planos de consulta em cache semelhantes. Os tempos de resposta de consulta podem ser mais previsíveis com atualizações de estatísticas assíncronas do que com atualizações de estatísticas síncronas, pois o otimizador de consulta pode executar consultas de entrada sem aguardar estatísticas atualizadas. Isso evita o atraso de algumas consultas e não de outras.  
  
-   Seu aplicativo excedeu o tempo limite de solicitações do cliente pelo fato de uma ou mais consultas estarem aguardando a atualização de estatísticas. Em alguns casos, a espera por estatísticas síncronas pode gerar falhas em aplicativos com tempo limite restrito.  
  
 INCREMENTAL STATS  
 Quando estiver ON, as estatísticas serão criadas por estatísticas de partição. Quando estiver OFF, a árvore de estatísticas será ignorada e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recomputará as estatísticas. O padrão é OFF. Essa configuração substitui a propriedade INCREMENTAL de nível de banco de dados.  
  
 Quando as novas partições são adicionados a uma tabela grande, as estatísticas devem ser atualizadas para incluir as novas partições. No entanto, o tempo necessário para digitalizar a tabela inteira (opção FULLSCAN ou SAMPLE) podem ser muito longos. Além disso, digitalizar a tabela inteira não é necessário porque somente as estatísticas nas novas partições podem ser necessárias. A opção incremental cria e armazena estatísticas por partição e, quando atualizada, somente atualiza estatísticas nessas partições que precisam de novas estatísticas  
  
 Se as estatísticas por partição não tiverem suporte, a opção será ignorada e um aviso será gerado. As estatísticas incrementais não têm suporte para os seguintes tipos de estatísticas:  
  
-   Estatísticas criadas com os índices que não estejam alinhados por partição com a tabela base.  
  
-   Estatísticas criadas em bancos de dados secundários legíveis AlwaysOn.  
  
-   Estatísticas criadas em bancos de dados somente leitura.  
  
-   Estatísticas criadas em índices filtrados.  
  
-   Estatísticas criadas em exibições.  
  
-   Estatísticas criadas em tabelas internas.  
  
-   Estatísticas criadas com índices espaciais ou índices XML.  
  
||  
|-|  
|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
  
##  <a name="CreateStatistics"></a> Quando criar estatísticas  
 O otimizador de consulta já cria estatísticas das seguintes maneiras:  
  
1.  O otimizador de consulta cria estatísticas para índices em tabelas ou exibições quando o índice é criado. Essas estatísticas são criadas nas colunas de chaves do índice. Se o índice for um índice filtrado, o otimizador de consulta criará estatísticas filtradas no mesmo subconjunto de linhas especificado para o índice filtrado. Para obter mais informações sobre índices filtrados, veja [Criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md) e [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
2.  O otimizador de consulta cria estatísticas para colunas únicas em predicados de consulta quando AUTO_CREATE_STATISTICS estiver ativada.  
  
 Para a maioria das consultas, esses dois métodos para criar estatísticas asseguram um plano de consulta de alta qualidade; em alguns casos, você pode aprimorar os planos de consulta criando estatísticas adicionais com a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) . Essas estatísticas adicionais podem capturar correlações estatísticas que o otimizador de consulta não considera ao criar estatísticas para índices ou colunas únicas. Seu aplicativo pode ter correlações estatísticas adicionais nos dados de tabela que, se calculadas em um objeto de estatísticas, pode permitir que o otimizador de consulta aprimore os planos de consulta. Por exemplo, estatísticas filtradas em um subconjunto de linhas de dados ou estatísticas multicolunas em colunas de predicado de consulta podem aprimorar o plano de consulta.  
  
 Ao criar estatísticas com a instrução CREATE STATISTICS, é recomendável manter a opção AUTO_CREATE_STATISTICS ativada de forma que o otimizador de consulta continue criando estatísticas da coluna única rotineiramente para colunas de predicado de consulta. Para obter mais informações sobre predicados de consulta, veja [Critério de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 Considere a criação de estatísticas com a instrução CREATE STATISTICS quando alguma das seguintes opções se aplicar:  
  
-   O Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] sugere a criação de estatísticas.  
  
-   O predicado de consulta contém várias colunas correlacionadas que ainda não estão no mesmo índice.  
  
-   A consulta faz a seleção em um subconjunto de dados.  
  
-   Há estatísticas ausentes na consulta.  
  
### <a name="query-predicate-contains-multiple-correlated-columns"></a>O predicado de consulta contém várias colunas correlacionadas  
 Quando um predicado de consulta contém várias colunas que têm relações e dependências entre colunas, as estatísticas nas várias colunas podem aprimorar o plano de consulta. As estatísticas em várias colunas contêm estatísticas de correlação entre colunas, chamadas *densidades*, que não estão disponíveis em estatísticas de coluna única. As densidades podem aprimorar as estimativas de cardinalidade quando os resultados de consulta dependem de relações de dados entre várias colunas.  
  
 Se as colunas já estiverem no mesmo índice, o objeto de estatísticas multicolunas já existirá e não será necessário criá-lo manualmente. Se as colunas ainda não estiverem no mesmo índice, você poderá criar estatísticas multicolunas criando um índice nas colunas ou usando a instrução CREATE STATISTICS. A manutenção de um índice exige mais recursos do sistema do que a de um objeto de estatísticas. Se o aplicativo não exigir o índice multicolunas, você poderá economizar recursos do sistema criando o objeto de estatísticas sem criar o índice.  
  
 Ao criar estatísticas multicolunas, a ordem das colunas na definição do objeto de estatísticas afeta a efetividade de densidades para calcular estimativas de cardinalidade. O objeto de estatísticas armazena densidades para cada prefixo de colunas de chave na definição do objeto. Para obter mais informações sobre densidades, veja [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).  
  
 Para criar densidades úteis para estimativas de cardinalidade, as colunas no predicado de consulta devem corresponder a um dos prefixos de colunas na definição do objeto de estatísticas. O exemplo a seguir cria um objeto de estatísticas multicolunas nas colunas `LastName`, `MiddleName`e `FirstName`.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.stats  
    WHERE name = 'LastFirst'  
    AND object_ID = OBJECT_ID ('Person.Person'))  
DROP STATISTICS Person.Person.LastFirst;  
GO  
CREATE STATISTICS LastFirst ON Person.Person (LastName, MiddleName, FirstName);  
GO  
```  
  
 Neste exemplo, o objeto de estatísticas `LastFirst` possui densidades para os seguintes prefixos de coluna: (`LastName`), (`LastName, MiddleName`) e (`LastName, MiddleName, FirstName`). A densidade não está disponível para (`LastName, FirstName`). Se a consulta usar `LastName` e `FirstName` sem usar `MiddleName`, a densidade não estará disponível para estimativas de cardinalidade.  
  
### <a name="query-selects-from-a-subset-of-data"></a>A consulta faz seleções em um subconjunto de dados  
 Quando o otimizador de consulta cria estatísticas para colunas únicas e índices, as estatísticas são criadas para os valores em todas as linhas. Quando as consultas fazem seleções em um subconjunto de linhas e esse subconjunto tem uma distribuição de dados exclusiva, as estatísticas filtradas podem aprimorar os planos de consulta. É possível criar estatísticas filtradas usando a instrução CREATE STATISTICS com a cláusula WHERE para definir a expressão de predicado de filtro.  
  
 Por exemplo, usando o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], cada produto da tabela Production.Product pertence a uma das quatro categorias da tabela Production.ProductCategory: Bicicletas, Componentes, Vestuário e Acessórios. Cada categoria possui uma distribuição de dados diferente para peso: as bicicletas pesam de 13,77 a 30, os componentes pesam de 2,12 a 1050,00 com alguns valores NULL, o peso de todas as roupas é NULL e o peso dos acessórios também é NULL.  
  
 Usando Bicicletas como um exemplo, as estatísticas filtradas em todos os pesos de bicicleta fornecerão estatísticas mais precisas ao otimizador de consultas e podem melhorar a qualidade do plano de consulta comparadas com as estatísticas de tabela completa ou estatísticas inexistentes na coluna Peso. A coluna de peso das bicicletas é uma boa candidata para estatísticas filtradas, mas não necessariamente para um índice filtrado se o número de pesquisas de peso for relativamente pequeno. O ganho de desempenho que um índice filtrado oferece às pesquisas pode não compensar os custos adicionais com a manutenção e o custo de armazenamento exigidos para adicionar um índice filtrado ao banco de dados.  
  
 A instrução a seguir cria as estatísticas filtradas de `BikeWeights` em todas as subcategorias de Bicicletas. A expressão de predicado filtrada define bicicletas enumerando todas as suas subcategorias com a comparação `Production.ProductSubcategoryID IN (1,2,3)`. O predicado não pode usar o nome de categoria Bicicletas porque ele está armazenado na tabela Production.ProductCategory e todas as colunas na expressão de filtro devem estar na mesma tabela.  
  
 [!code-sql[StatisticsDDL#FilteredStats2](../../relational-databases/statistics/codesnippet/tsql/statistics_1.sql)]  
  
 O otimizador de consulta pode usar as estatísticas filtradas de `BikeWeights` para aprimorar o plano da consulta a seguir, que seleciona todas as bicicletas que pesam mais de `25`.  
  
```  
SELECT P.Weight AS Weight, S.Name AS BikeName  
FROM Production.Product AS P  
    JOIN Production.ProductSubcategory AS S   
    ON P.ProductSubcategoryID = S.ProductSubcategoryID  
WHERE P.ProductSubcategoryID IN (1,2,3) AND P.Weight > 25  
ORDER BY P.Weight;  
GO  
```  
  
### <a name="query-identifies-missing-statistics"></a>A consulta identifica estatísticas ausentes  
 Se um erro ou outro evento impedir que o otimizador de consulta crie estatísticas, o otimizador criará o plano de consulta sem usar estatísticas. O otimizador de consulta marca as estatísticas como ausentes e tenta gerar as estatísticas novamente na próxima execução da consulta.  
  
 As estatísticas ausentes são indicadas como avisos (nome de tabela em texto vermelho) quando o plano de execução de uma consulta é exibido graficamente usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Além disso, o monitoramento da classe de evento **Missing Column Statistics** usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] indica quando há estatísticas ausentes. Para obter mais informações, veja [Categoria de evento de erros e de avisos &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/event-classes/errors-and-warnings-event-category-database-engine.md).  
  
 Se houver estatísticas ausentes, execute as seguintes etapas:  
  
-   Verifique se AUTO_CREATE_STATISTICS e AUTO_UPDATE_STATISTICS estão ativadas.  
  
-   Verifique se o banco de dados não é somente leitura. Se o banco de dados for somente leitura, o otimizador de consulta não poderá salvar estatísticas.  
  
-   Crie as estatísticas ausentes usando a instrução CREATE STATISTICS.  
  
 Quando as estatísticas em um banco de dados somente leitura ou um instantâneo somente leitura estão ausentes ou obsoletas, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria e mantém estatísticas temporárias no **tempdb**. Quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria estatísticas temporárias, o nome das estatísticas é anexado com o sufixo _readonly_database_statistic para diferenciar as estatísticas temporárias de estatísticas permanentes. O sufixo _readonly_database_statistic fica reservado para estatísticas geradas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. É possível criar e reproduzir scripts para as estatísticas temporárias em um banco de dados de leitura-gravação. Quando em script, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] altera o sufixo do nome das estatísticas de _readonly_database_statistic para _readonly_database_statistic_scripted.  
  
 Somente o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode criar e atualizar estatísticas temporárias. No entanto, você pode excluir estatísticas temporárias e monitorar as propriedades de estatísticas que usam as mesmas ferramentas que você utiliza para estatísticas permanentes:  
  
-   Exclua estatísticas temporárias usando a instrução [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md) .  
  
-   Para monitorar as estatísticas, use as exibições de catálogo **sys.stats** e **sys.stats_columns** . **sys_stats** inclui a coluna, **is_temporary** para indicar quais estatísticas são permanentes e quais são temporárias.  
  
 Como as estatísticas temporárias são armazenadas em **tempdb**, uma reinicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz com que todas as estatísticas temporárias desapareçam.  
  
  
##  <a name="UpdateStatistics"></a> Quando atualizar estatísticas  
 O otimizador de consulta determina quando as estatísticas podem estar desatualizadas e as atualiza quando forem necessárias para um plano de consulta. Em alguns casos, você pode aprimorar o plano de consulta e, portanto, o desempenho da consulta por meio da atualização mais frequente das estatísticas do que quando AUTO_UPDATE_STATISTICS está ativada. Você pode atualizar estatísticas com a instrução UPDATE STATISTICS ou o procedimento armazenado sp_updatestats.  
  
 A atualização de estatísticas assegura que as consultas sejam compiladas com estatísticas atualizadas. Porém, a atualização de estatísticas faz com que as consultas sejam recompiladas. É recomendável não atualizar estatísticas com muita frequência porque existe uma compensação de desempenho entre o aprimoramento dos planos de consulta e o tempo necessário para recompilar consultas. As compensações específicas dependem do seu aplicativo.  
  
 Quando você atualizar estatísticas com UPDATE STATISTICS ou sp_updatestats, recomendamos manter a opção AUTO_UPDATE_STATISTICS ativada de forma que o otimizador de consultas continue a atualizar estatísticas periodicamente. Para obter mais informações sobre como atualizar estatísticas em uma coluna, um índice, uma tabela ou uma exibição indexada, veja [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md). Para obter informações sobre como atualizar estatísticas de todas as tabelas definidas pelo usuário e internas no banco de dados, veja o procedimento armazenado [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md).  
  
 Para determinar quando as estatísticas foram atualizadas pela última vez, use a função [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) .  
  
 Considere a atualização de estatísticas nas seguintes condições:  
  
-   Os tempos de execução de consulta estão lentos.  
  
-   As operações de inserção ocorrem em colunas de chaves crescentes ou decrescentes.  
  
-   Após operações de manutenção.  
  
### <a name="query-execution-times-are-slow"></a>Os tempos de execução de consulta estão lentos  
 Se os tempos de resposta de consultas estiverem lentos ou imprevisíveis, verifique se as consultas têm estatísticas atualizadas antes de executar as etapas adicionais de solução de problemas.  
  
### <a name="insert-operations-occur-on-ascending-or-descending-key-columns"></a>As operações de inserção ocorrem em colunas de chaves crescentes ou decrescentes  
 As estatísticas em colunas de chaves crescentes ou decrescentes, como colunas IDENTITY ou colunas de carimbo de data/hora em tempo real, podem exigir atualizações de estatísticas mais frequentes do que as executadas pelo otimizador de consulta. As operações de inserção acrescentam novos valores às colunas crescentes ou decrescentes. O número de linhas adicionadas pode ser muito pequeno para disparar uma atualização de estatísticas. Se as estatísticas não estiverem atualizadas e as consultas fizerem seleções nas linhas adicionadas mais recentemente, as estatísticas atuais não terão estimativas de cardinalidade para obter esses novos valores. Isso pode resultar em estimativas de cardinalidade imprecisas e lentidão no desempenho de consulta.  
  
 Por exemplo, uma consulta que faz seleções em ordens de venda com as datas mais recentes terá estimativas de cardinalidade imprecisas, se as estatísticas não forem atualizadas para incluir estimativas de cardinalidade dessas ordens de venda.  
  
### <a name="after-maintenance-operations"></a>Após operações de manutenção  
 Considere a atualização de estatísticas depois de executar procedimentos de manutenção que alteram a distribuição de dados, como truncar uma tabela ou executar uma inserção em massa de uma porcentagem grande das linhas. Isso pode evitar futuros atrasos no processamento de consultas enquanto elas aguardam atualizações de estatísticas automáticas.  
  
 Operações como reconstrução, desfragmentação ou reorganização de um índice não alteram a distribuição de dados. Portanto, não é necessário atualizar estatísticas depois de executar as operações ALTER INDEX REBUILD, DBCC REINDEX, DBCC INDEXDEFRAG ou ALTER INDEX REORGANIZE. O otimizador de consulta atualiza estatísticas quando você reconstrói um índice em uma tabela ou exibição com ALTER INDEX REBUILD ou DBCC DBREINDEX; porém, essa atualização de estatísticas é um subproduto da recriação do índice. O otimizador de consulta não atualiza estatísticas depois de operações DBCC INDEXDEFRAG ou ALTER INDEX REORGANIZE.  
  
  
##  <a name="DesignStatistics"></a> Consultas que usam estatísticas com eficiência  
 Algumas implementações de consulta, como variáveis locais e expressões complexas no predicado de consulta, podem gerar planos de consulta de qualidade inferior. O cumprimento das diretrizes de design de consulta para o uso eficiente de estatísticas pode ajudar a evitar esse problema. Para obter mais informações sobre predicados de consulta, veja [Critério de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 Você pode melhorar planos de consulta aplicando diretrizes de design de consulta que usam estatísticas de modo eficiente para aprimorar *estimativas de cardinalidade* para expressões, variáveis e funções usadas em predicados de consulta. Quando o otimizador de consulta não souber o valor de uma expressão, variável ou função, ele não saberá qual o valor a ser pesquisado no histograma e, portanto, não poderá recuperar a melhor estimativa de cardinalidade do histograma. Em vez disso, o otimizador de consulta baseia a estimativa de cardinalidade no número médio de linhas por valor distinto de todas as linhas de amostra no histograma. Isso gera estimativas de cardinalidade de qualidade inferior e pode prejudicar o desempenho de consulta.  
  
 As diretrizes a seguir descrevem como escrever consultas para melhorar planos de consulta por meio do aprimoramento das estimativas de cardinalidade.  
  
### <a name="improving-cardinality-estimates-for-expressions"></a>Aprimorando estimativas de cardinalidade para expressões  
 Para aprimorar as estimativas de cardinalidade para expressões, siga estas diretrizes:  
  
-   Sempre que possível, simplifique expressões com constantes. O otimizador de consulta não avalia todas as funções e expressões que contêm constantes antes de determinar as estimativas de cardinalidade. Por exemplo, simplifique a expressão ABS (`-100) to 100`.  
  
-   Se a expressão usar muitas variáveis, considere a criação de uma coluna computada para a expressão e crie estatísticas ou um índice na coluna computada. Por exemplo, o predicado de consulta `WHERE PRICE + Tax > 100` poderá ter uma estimativa de cardinalidade melhor se você criar uma coluna computada para a expressão `Price + Tax`.  
  
### <a name="improving-cardinality-estimates-for-variables-and-functions"></a>Melhorando estimativas de cardinalidade para variáveis e funções  
 Para melhorar as estimativas de cardinalidade para variáveis e funções, siga estas diretrizes:  
  
-   Se o predicado de consulta usar uma variável local, considere reescrever a consulta para usar um parâmetro em vez de uma variável local. O valor de uma variável local não é conhecido quando o otimizador de consulta cria o plano de execução de consulta. Quando uma consulta usar um parâmetro, o otimizador de consulta usará a estimativa de cardinalidade para o primeiro valor de parâmetro real transmitido ao procedimento armazenado.  
  
-   Considere o uso de uma tabela padrão ou uma tabela temporária para manter os resultados de funções com valor de tabela de várias instruções. O otimizador de consulta não cria estatísticas para funções com valor de tabela de várias instruções. Com essa abordagem, o otimizador de consulta pode criar estatísticas nas colunas de tabela e usá-las para criar um plano de consulta melhor.  
  
-   Considere o uso de uma tabela padrão ou uma tabela temporária como uma substituição para variáveis de tabela. O otimizador de consulta não cria estatísticas para variáveis de tabela. Com essa abordagem, o otimizador de consulta pode criar estatísticas nas colunas de tabela e usá-las para criar um plano de consulta melhor. Há compensações ao optar pelo uso de uma tabela temporária ou de uma variável de tabela; as variáveis de tabela usadas em procedimentos armazenados causam menos recompilações do procedimento armazenado que as tabelas temporárias. Dependendo do aplicativo, o uso de uma tabela temporária em vez de uma variável de tabela pode não melhorar o desempenho.  
  
-   Se um procedimento armazenado contiver uma consulta que usa um parâmetro transmitido, evite alterar o valor de parâmetro no procedimento armazenado antes de usá-lo na consulta. As estimativas de cardinalidade da consulta se baseiam no valor de parâmetro transmitido, não no valor atualizado. Para evitar alterar o valor do parâmetro, você pode reescrever a consulta para usar dois procedimentos armazenados.  
  
     Por exemplo, o procedimento armazenado `Sales.GetRecentSales` a seguir altera o valor do parâmetro `@date` quando `@date is NULL`.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
     Se a primeira chamada do procedimento armazenado `Sales.GetRecentSales` transmitir NULL para o parâmetro `@date` , o otimizador de consulta compilará o procedimento armazenado com a estimativa de cardinalidade para `@date = NULL` , embora o predicado de consulta não seja chamado com `@date = NULL`. Essa estimativa de cardinalidade pode ser significativamente diferente do número de linhas no resultado de consulta real. Como resultado, o otimizador de consulta pode escolher um plano de consulta de qualidade inferior. Para evitar isso, você pode reescrever o procedimento armazenado em dois procedimentos da seguinte maneira:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNullRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        EXEC Sales.GetNonNullRecentSales @date;  
    END  
    GO  
    IF OBJECT_ID ( 'Sales.GetNonNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNonNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNonNullRecentSales (@date datetime)  
    AS BEGIN  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
### <a name="improving-cardinality-estimates-with-query-hints"></a>Melhorando estimativas de cardinalidade com dicas de consulta  
 Para melhorar estimativas de cardinalidade para variáveis locais, você pode usar as dicas de consulta OPTIMIZE FOR ou OPTIMIZE FOR UNKNOWN com RECOMPILE. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
 Para alguns aplicativos, a recompilação da consulta toda vez que ela é executada pode levar muito tempo. A dica de consulta OPTIMIZER FOR poderá ajudar, mesmo que você não use a opção RECOMPILE. Por exemplo, você poderia acrescentar uma opção OPTIMIZER FOR ao procedimento armazenado Sales.GetRecentSales para especificar uma data específica. O exemplo a seguir acrescenta a opção OPTIMIZE FOR ao procedimento Sales.GetRecentSales.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetRecentSales;  
GO  
CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
AS BEGIN  
    IF @date is NULL  
        SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
    SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
    WHERE h.SalesOrderID = d.SalesOrderID  
    AND h.OrderDate > @date  
    OPTION ( OPTIMIZE FOR ( @date = '2004-05-01 00:00:00.000'))  
END;  
GO  
```  
  
### <a name="improving-cardinality-estimates-with-plan-guides"></a>Melhorando estimativas de cardinalidade com guias de plano  
 Para alguns aplicativos, é possível que as diretrizes de design de consulta não se apliquem porque você não pode alterar a consulta ou porque o uso da dica de consulta RECOMPILE pode causar muitas recompilações. Você pode usar guias de plano para especificar outras dicas, como USE PLAN, a fim de controlar o comportamento da consulta ao investigar alterações do aplicativo com o fornecedor do aplicativo. Para obter mais informações sobre guias de plano, consulte [Plan Guides](../../relational-databases/performance/plan-guides.md).  
  
  
## <a name="see-also"></a>Consulte também  
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [Criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md)  
  
  

