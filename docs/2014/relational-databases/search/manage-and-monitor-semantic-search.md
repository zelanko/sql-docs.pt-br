---
title: Gerenciar e monitorar a pesquisa semântica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], managing
- semantic search [SQL Server], monitoring
ms.assetid: eb5c3b29-da70-42aa-aa97-7d35a3f1eb98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 94f8edc0fe8b2505adc36705200e299f36b2dbf9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011127"
---
# <a name="manage-and-monitor-semantic-search"></a>Gerenciar e monitorar a pesquisa semântica
  Descreve o processo de indexação semântica e as tarefas relacionadas ao gerenciamento e monitoramento dos índices.  
  
##  <a name="HowToMonitorStatus"></a>Como verificar o status da indexação semântica  
 **A primeira fase da indexação semântica está concluída?**  
 Consulte a exibição de gerenciamento dinâmico [sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql) e verifique as colunas **status** e **status_description**.  
  
 A primeira fase da indexação inclui a população do índice de palavras-chave de texto completo e o índice de frases-chave semântico, além da extração de dados de similaridade de documentos.  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
 **A segunda fase da indexação semântica está concluída?**  
 Consulte a exibição de gerenciamento dinâmico [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql) e verifique as colunas **status** e **status_description**.  
  
 A segunda fase da indexação inclui a população do índice semântico de similaridade de documentos.  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="HowToCheckSize"></a>Como verificar o tamanho dos índices semânticos  
 **Qual é o tamanho lógico de um índice semântico de frases-chave ou um índice semântico de similaridade de documentos?**  
 Consulte a exibição de gerenciamento dinâmico [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql).  
  
 O tamanho lógico é exibido em número de páginas de índice.  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
 **Qual é o tamanho total dos índices de texto completo e semântico para um catálogo de texto completo?**  
 Consulta a propriedade **IndexSize** da função de metadados [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql).  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
 **Quantos itens são indexados nos índices de texto completo e semântico para um catálogo de texto completo?**  
 Consulta a propriedade **ItemCount** da função de metadados [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql).  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="HowToForcePopulation"></a>Como forçar a população dos índices semânticos  
 Você pode forçar a população de índices de texto completo e semânticos usando a cláusula START/STOP/PAUSE ou RESUME POPULATION com a mesma sintaxe e o comportamento descrito para índices de texto completo. Para obter mais informações, veja [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql) e [Popular índices de texto completo](../indexes/indexes.md).  
  
 Como a indexação semântica é dependente da indexação de texto completo, os índices semânticos são populados apenas quando os índices de texto completo associados são populados.  
  
 **Exemplo: iniciar uma população completa de índices de texto completo e semânticos**  
  
 O exemplo a seguir inicia a população completa de índices de texto completo e semânticos alterando um índice de texto completo existente na tabela **Production.Document** no banco de dados de exemplo AdventureWorks2012.  
  
```vb  
USE AdventureWorks2012  
GO  
  
ALTER FULLTEXT INDEX ON Production.Document  
    START FULL POPULATION  
GO  
```  
  
##  <a name="HowToDisableIndexing"></a>Como desabilitar ou reabilitar a indexação semântica  
 Você pode habilitar ou desabilitar a indexação de texto completo ou semântica usando a cláusula ENABLE/DISABLE com a mesma sintaxe e o comportamento descrito para índices de texto completo. Para obter mais informações, consulte [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql).  
  
 Quando a indexação semântica é desabilitada e suspensa, as consultas em dados semânticos continuam a funcionar com êxito e retornar dados previamente indexados. Esse comportamento não é consistente com o comportamento da Pesquisa de Texto Completo.  
  
```sql  
-- To disable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name DISABLE  
GO  
  
-- To re-enable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name ENABLE  
GO  
```  
  
##  <a name="SemanticIndexing"></a>Fases de Indexação semântica  
 A Pesquisa Semântica indexa dois tipos de dados para cada coluna na qual está habilitada:  
  
1.  **Frases-chave**  
  
2.  **Similaridade de documentos**  
  
 A indexação semântica ocorre em duas fases, junto com a indexação de texto completo:  
  
1.  **Fase 1**. O índice de palavras-chave de texto completo e o índice de frases-chave semântico são populados ao mesmo tempo em paralelo. Os dados necessários para indexar a similaridade de documentos também são extraídos neste momento.  
  
2.  **Fase 2**. O índice semântico de similaridade de documentos é então populado. Esse índice depende de ambos os índices que foram populados na fase anterior.  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="ProblemNotPopulated"></a>Problema: os índices semânticos não são populados  
 **Os índices de texto completo associados estão populados?**  
 Como a indexação semântica é dependente da indexação de texto completo, os índices semânticos são populados apenas quando os índices de texto completo associados são populados.  
  
 **As pesquisas de texto completo e semântica estão instaladas e configuradas corretamente?**  
 Para obter mais informações, veja [Instalar e configurar a pesquisa semântica](install-and-configure-semantic-search.md).  
  
 **O serviço FDHOST não está disponível ou há outra condição que cause a falha da indexação de texto completo?**  
 Para obter mais informações, veja [Solucionar problemas na indexação de texto completo](troubleshoot-full-text-indexing.md).  
  
  
