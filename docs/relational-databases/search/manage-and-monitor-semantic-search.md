---
title: Gerenciar e monitorar a pesquisa semântica | Microsoft Docs
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], managing
- semantic search [SQL Server], monitoring
ms.assetid: eb5c3b29-da70-42aa-aa97-7d35a3f1eb98
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: c5e5c8256c117ebd3fbb57b5a7c291b539c5a428
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68132249"
---
# <a name="manage-and-monitor-semantic-search"></a>Gerenciar e monitorar a pesquisa semântica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Descreve o processo de indexação semântica e as tarefas relacionadas ao gerenciamento e monitoramento dos índices.  
  
##  <a name="HowToMonitorStatus"></a> Verificar o status da indexação semântica  
### <a name="is-the-first-phase-of-semantic-indexing-complete"></a>A primeira fase da indexação semântica está concluída?
 Consulte a exibição de gerenciamento dinâmico [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md) e verifique as colunas **status** e **status_description**.  
  
 A primeira fase da indexação inclui a população do índice de palavras-chave de texto completo e o índice de frases-chave semântico, além da extração de dados de similaridade de documentos.  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="is-the-second-phase-of-semantic-indexing-complete"></a>A segunda fase da indexação semântica está concluída?
 Consulte a exibição de gerenciamento dinâmico [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md) e verifique as colunas **status** e **status_description**.  
  
 A segunda fase da indexação inclui a população do índice semântico de similaridade de documentos.  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="HowToCheckSize"></a> Verificar o tamanho dos índices semânticos  
### <a name="what-is-the-logical-size-of-a-semantic-key-phrase-index-or-a-semantic-document-similarity-index"></a>Qual é o tamanho lógico de um índice semântico de frases-chave ou um índice semântico de similaridade de documentos?
 Consulte a exibição de gerenciamento dinâmico [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md).  
  
 O tamanho lógico é exibido em número de páginas de índice.  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="what-is-the-total-size-of-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>Qual é o tamanho total dos índices de texto completo e semântico para um catálogo de texto completo?  
 Consulta a propriedade **IndexSize** da função de metadados [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md).  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
### <a name="how-many-items-are-indexed-in-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>Quantos itens são indexados nos índices de texto completo e semântico para um catálogo de texto completo?  
 Consulta a propriedade **ItemCount** da função de metadados [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md).  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="HowToForcePopulation"></a> Forçar a população dos índices semânticos  
 Você pode forçar a população de índices de texto completo e semânticos usando a cláusula START/STOP/PAUSE ou RESUME POPULATION com a mesma sintaxe e o comportamento descrito para índices de texto completo. Para obter mais informações, veja [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md) e [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
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
  
##  <a name="HowToDisableIndexing"></a> Desabilitar ou reabilitar a indexação semântica  
 Você pode habilitar ou desabilitar a indexação de texto completo ou semântica usando a cláusula ENABLE/DISABLE com a mesma sintaxe e o comportamento descrito para índices de texto completo. Para obter mais informações, consulte [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
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
  
##  <a name="SemanticIndexing"></a> Sobre as fases de indexação semântica  
 A Pesquisa Semântica indexa dois tipos de dados para cada coluna na qual está habilitada:  
  
1.  **Frases-chave**  
  
2.  **Similaridade de documentos**  
  
 A indexação semântica ocorre em duas fases, junto com a indexação de texto completo:  
  
1.  **Fase 1**. O índice de palavras-chave de texto completo e o índice de frases-chave semântico são populados ao mesmo tempo em paralelo. Os dados necessários para indexar a similaridade de documentos também são extraídos neste momento.  
  
2.  **Fase 2**. O índice semântico de similaridade de documentos é então populado. Esse índice depende de ambos os índices que foram populados na fase anterior.  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="ProblemNotPopulated"></a> Problema: Os índices semânticos não são populados  
### <a name="are-the-associated-full-text-indexes-populated"></a>Os índices de texto completo associados estão populados?  
 Como a indexação semântica é dependente da indexação de texto completo, os índices semânticos são populados apenas quando os índices de texto completo associados são populados.  
  
### <a name="are-full-text-search-and-semantic-search-properly-installed-and-configured"></a>As pesquisas de texto completo e semântica estão instaladas e configuradas corretamente?  
 Para obter mais informações, veja [Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
### <a name="is-the-fdhost-service-not-available-or-is-there-another-condition-that-would-cause-full-text-indexing-to-fail"></a>O serviço FDHOST não está disponível ou há outra condição que cause a falha da indexação de texto completo?  
 Para obter mais informações, veja [Solucionar problemas na indexação de texto completo](../../relational-databases/search/troubleshoot-full-text-indexing.md).  
  
  
