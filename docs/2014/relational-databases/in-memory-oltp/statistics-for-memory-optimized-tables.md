---
title: Estatísticas para tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: d4f9da688927d7e96ac2162eb504e0bc15f27526
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008168"
---
# <a name="statistics-for-memory-optimized-tables"></a>Estatísticas para tabelas com otimização de memória
  O otimizador de consulta usa estatísticas sobre colunas para criar planos de consulta que melhoram o desempenho das consultas. As estatísticas são coletadas de tabelas no banco de dados e armazenadas nos metadados do banco de dados.  
  
 As estatísticas são criadas automaticamente, mas também podem ser criadas manualmente. Por exemplo, as estatísticas são criadas automaticamente para colunas de chave de índice durante a criação do índice. Para obter mais informações sobre como criar estatísticas, consulte [Statistics](../statistics/statistics.md).  
  
 Geralmente, os dados de tabela são alterados com o tempo, à medida que linhas são inseridas, atualizadas e excluídas. Isso significa que as estatísticas precisam ser atualizadas periodicamente. Por padrão, as estatísticas em tabelas baseadas em disco são atualizadas automaticamente quando o otimizador determina que elas podem estar desatualizadas.  
  
 As estatísticas sobre tabelas com otimização de memória não são atualizadas por padrão. É preciso atualizá-las manualmente. Use [UPDATE STATISTICS &#40;Transact-SQL&#41; ](/sql/t-sql/statements/update-statistics-transact-sql) para colunas individuais, índices ou tabelas. Use [sp_updatestats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) para atualizar as estatísticas para todos os usuários e as tabelas internas no banco de dados.  
  
 Ao usar [CREATE STATISTICS &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-statistics-transact-sql) ou [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql), você deve especificar `NORECOMPUTE` para desabilitar automática de estatísticas atualização para tabelas com otimização de memória. Para tabelas baseadas em disco, [sp_updatestats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) atualizará as estatísticas somente se a tabela tiver sido modificada desde a última [sp_updatestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql). Para tabelas com otimização de memória, [sp_updatestats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) sempre gera estatísticas atualizadas. [sp_updatestats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) é uma boa opção para tabelas com otimização de memória; caso contrário, você precisa saber quais tabelas têm alterações significativas para que você possa atualizar estatísticas individualmente.  
  
 As estatísticas podem ser geradas pela amostragem dos dados ou executando um exame completo. As estatísticas por amostra usam apenas uma amostra dos dados da tabela para estimar a distribuição de dados. As estatísticas por exame completo verificam a tabela inteira para determinar a distribuição de dados. As estatísticas por exame completo geralmente são mais precisas, mas levam mais tempo para serem calculadas. As estatísticas por amostra podem ser coletadas mais rapidamente.  
  
 As tabelas baseadas em disco usam estatísticas por amostra, por padrão. As tabelas com otimização de memória oferecem suporte apenas às estatísticas por exame completo. Ao usar [CREATE STATISTICS &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-statistics-transact-sql) ou [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql), você deve especificar o `FULLSCAN` opção para otimização de memória tabelas.  
  
 Considerações adicionais para estatísticas em tabelas com otimização de memória:  
  
-   Os índices nas tabelas com otimização de memória são criados com a tabela. As estatísticas nas colunas de chave de índice são criadas quando a tabela está vazia. Desse modo, essas estatísticas precisam ser atualizadas depois que os dados são isolados na tabela.  
  
-   Para procedimentos armazenados compilados nativamente, os planos de execução para consultas no procedimento são otimizados quando o procedimento é compilado. Isso acontece somente quando o procedimento é criado e quando o servidor é reiniciado, e não quando as estatísticas são atualizadas. Consequentemente, as tabelas precisam conter um conjunto de dados representativo, e as estatísticas precisam ser atualizadas antes que os procedimentos sejam criados. (Os procedimentos armazenados compilados nativamente serão recompilados se o banco de dados ficar offline e voltar a ficar online ou se houver uma reinicialização do servidor.)  
  
## <a name="guidelines-for-statistics-when-deploying-memory-optimized-tables"></a>Diretrizes para estatísticas ao implantar tabelas com otimização de memória  
 Para garantir que o otimizador de consulta tenha estatísticas atualizadas durante a criação de planos de consulta, implante tabelas com otimização de memória usando estas cinco etapas:  
  
1.  Crie tabelas e índices. Os índices são especificados em linha no `CREATE TABLE` instruções.  
  
2.  Carregue dados nas tabelas.  
  
3.  Atualize as estatísticas nas tabelas.  
  
4.  Crie procedimentos armazenados que acessam as tabelas.  
  
5.  Executar a carga de trabalho, que pode conter uma mistura de interpretado e compilados nativamente [!INCLUDE[tsql](../../../includes/tsql-md.md)] armazenados, procedimentos, bem como lotes ad hoc.  
  
 A criação de procedimentos armazenados compilados nativamente após o carregamento dos dados e a atualização das estatísticas garante que o otimizador tenha estatísticas disponíveis para as tabelas com otimização de memória. Isso garantirá planos de consulta eficientes quando o procedimento for compilado.  
  
## <a name="guidelines-for-maintaining-statistics-on-memory-optimized-tables"></a>Diretrizes para manter estatísticas em tabelas com otimização de memória  
 Para manter as estatísticas atualizadas, atualize-as regularmente nas tabelas com otimização de memória.  
  
 Se os dados são alterados frequentemente, você deve atualizar as estatísticas com frequência. Por exemplo, atualize as estatísticas da tabelas após uma atualização do lote. Depois de atualizar as estatísticas, descarte e recrie os procedimentos armazenados compilados nativamente para que eles possam se beneficiar das estatísticas atualizadas.  
  
 para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
 Não atualize as estatísticas durante picos de carga de trabalho.  
  
 Para atualizar estatísticas:  
  
-   Use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para [criar um plano de manutenção](../maintenance-plans/create-a-maintenance-plan.md) com um [estatística de tarefa de atualização](../maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
-   Ou atualize estatísticas usando um script [!INCLUDE[tsql](../../../includes/tsql-md.md)], conforme discutido abaixo.  
  
 Para atualizar as estatísticas de uma única tabela com otimização de memória (*myschema*. *Mytable*), execute o seguinte script:  
  
```  
UPDATE STATISTICS myschema.Mytable WITH FULLSCAN, NORECOMPUTE  
```  
  
 Para atualizar estatísticas de todas as tabelas com otimização de memória no banco de dados atual, execute o seguinte script:  
  
```tsql  
DECLARE @sql NVARCHAR(MAX) = N''  
  
SELECT @sql += N'  
   UPDATE STATISTICS ' + quotename(schema_name(schema_id)) + N'.' + quotename(name) + N' WITH FULLSCAN, NORECOMPUTE'  
FROM sys.tables WHERE is_memory_optimized=1  
  
EXEC sp_executesql @sql  
```  
  
 Para atualizar as estatísticas de todas as tabelas no banco de dados, execute [sp_updatestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql).  
  
 O exemplo a seguir relata quando as estatísticas em tabelas com otimização de memória foram atualizadas pela última vez. Essas informações podem ajudá-lo a decidir se você precisar atualizar as estatísticas.  
  
```tsql  
select t.object_id, t.name, sp.last_updated as 'stats_last_updated'  
from sys.tables t join sys.stats s on t.object_id=s.object_id cross apply sys.dm_db_stats_properties(t.object_id, s.stats_id) sp  
where t.is_memory_optimized=1  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas com otimização de memória](memory-optimized-tables.md)  
  
  
