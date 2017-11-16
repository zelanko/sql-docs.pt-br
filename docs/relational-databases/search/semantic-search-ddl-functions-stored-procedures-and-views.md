---
title: "Pesquisa de semântica de DDL, funções, procedimentos armazenados e exibições | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: semantic search [SQL Server], database objects
ms.assetid: 182f395f-3168-48a4-b723-ef4403544f9f
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b54e6187b386220fd6f9026358ef22522390ea94
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="semantic-search-ddl-functions-stored-procedures-and-views"></a>Pesquisa de semântica DDL, funções, procedimentos armazenados e exibições
  Lista as instruções Transact-SQL e os objetos de banco de dados que oferecem suporte à pesquisa semântica estatística no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter a lista de instruções e objetos de banco de dados que dão suporte à pesquisa de texto completo, consulte [DDL, funções, procedimentos armazenados e exibições de pesquisa de texto completo](../../relational-databases/search/full-text-search-ddl-functions-stored-procedures-and-views.md).  
  
##  <a name="ddl"></a> Instruções DDL (linguagem de definição de dados)  
  
|Objeto|Mais informações|  
|------------|----------------------|  
|[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)|[Habilitar a pesquisa semântica em tabelas e colunas](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)|  
|[CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)|[Habilitar a pesquisa semântica em tabelas e colunas](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)|  
  
##  <a name="func"></a> Funções de sistema  
  
|Objeto|Mais informações|  
|------------|----------------------|  
|[semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)|[Localizar frases chave em documentos com pesquisa semântica](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)|  
|[semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)|[Localizar documentos semelhantes e relacionados com a pesquisa semântica](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)|  
|[semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)|[Localizar documentos semelhantes e relacionados com a pesquisa semântica](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)|  
  
##  <a name="meta"></a> Funções de metadados do sistema  
  
|Objeto|Mais informações|  
|------------|----------------------|  
|[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)|[Habilitar a pesquisa semântica em tabelas e colunas](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)|  
|[DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)|[Habilitar a pesquisa semântica em tabelas e colunas](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)|  
|[FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)|[Gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
|[INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)|[Gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)|[Habilitar a pesquisa semântica em tabelas e colunas](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)|[Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md)|  
  
##  <a name="sproc"></a> Procedimentos armazenados do sistema  
  
|Objeto|Mais informações|  
|------------|----------------------|  
|[sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md)|[Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md)|  
|[sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md)|[Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md)|  
  
##  <a name="cv"></a> Exibições do catálogo  
  
|Objeto|Mais informações|  
|------------|----------------------|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)|[Gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
|[sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)|[Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md)|  
|[sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)|[Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md)|  
  
##  <a name="dmv"></a> Exibições de gerenciamento dinâmico  
  
|Objeto|Mais informações|  
|------------|----------------------|  
|[sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)|[Gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)|[Gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)|[Gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
