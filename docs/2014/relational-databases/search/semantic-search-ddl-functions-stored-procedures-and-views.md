---
title: Pesquisa de semântica de DDL, funções, procedimentos armazenados e exibições | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], database objects
ms.assetid: 182f395f-3168-48a4-b723-ef4403544f9f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 76ced95f53b50c0fc0402051cff35329d39ce9f0
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52530737"
---
# <a name="semantic-search-ddl-functions-stored-procedures-and-views"></a>Pesquisa de semântica DDL, funções, procedimentos armazenados e exibições
  Lista as instruções Transact-SQL e os objetos de banco de dados que oferecem suporte à pesquisa semântica estatística no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter a lista de instruções e objetos de banco de dados que dão suporte à pesquisa de texto completo, consulte [DDL, funções, procedimentos armazenados e exibições de pesquisa de texto completo](../views/views.md).  
  
##  <a name="ddl"></a> Instruções DDL (linguagem de definição de dados) Transact-SQL  
  
|Object|Mais Informações|  
|------------|----------------------|  
|[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)|[Habilitar a pesquisa semântica em tabelas e colunas](enable-semantic-search-on-tables-and-columns.md)|  
|[CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)|[Habilitar a pesquisa semântica em tabelas e colunas](enable-semantic-search-on-tables-and-columns.md)|  
  
##  <a name="func"></a> Funções de sistema  
  
|Object|Mais Informações|  
|------------|----------------------|  
|[semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql)|[Localizar frases chave em documentos com a pesquisa semântica](find-key-phrases-in-documents-with-semantic-search.md)|  
|[semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql)|[Localizar documentos semelhantes e relacionados com a pesquisa semântica](find-similar-and-related-documents-with-semantic-search.md)|  
|[semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql)|[Localizar documentos semelhantes e relacionados com a pesquisa semântica](find-similar-and-related-documents-with-semantic-search.md)|  
  
##  <a name="meta"></a> Funções de metadados do sistema  
  
|Object|Mais Informações|  
|------------|----------------------|  
|[COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)|[Habilitar a pesquisa semântica em tabelas e colunas](enable-semantic-search-on-tables-and-columns.md)|  
|[DATABASEPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql)|[Habilitar a pesquisa semântica em tabelas e colunas](enable-semantic-search-on-tables-and-columns.md)|  
|[FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)|[Gerenciar e monitorar a pesquisa semântica](manage-and-monitor-semantic-search.md)|  
|[INDEXPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/indexproperty-transact-sql)|[Gerenciar e monitorar a pesquisa semântica](manage-and-monitor-semantic-search.md)|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|[Habilitar a pesquisa semântica em tabelas e colunas](enable-semantic-search-on-tables-and-columns.md)|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|[Instalar e configurar a pesquisa semântica](install-and-configure-semantic-search.md)|  
  
##  <a name="sproc"></a> Procedimentos armazenados do sistema  
  
|Object|Mais Informações|  
|------------|----------------------|  
|[sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql)|[Instalar e configurar a pesquisa semântica](install-and-configure-semantic-search.md)|  
|[sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql)|[Instalar e configurar a pesquisa semântica](install-and-configure-semantic-search.md)|  
  
##  <a name="cv"></a> Exibições do sistema – Exibições do catálogo  
  
|Object|Mais Informações|  
|------------|----------------------|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|[Gerenciar e monitorar a pesquisa semântica](manage-and-monitor-semantic-search.md)|  
|[sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql)|[Instalar e configurar a pesquisa semântica](install-and-configure-semantic-search.md)|  
|[sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql)|[Instalar e configurar a pesquisa semântica](install-and-configure-semantic-search.md)|  
  
##  <a name="dmv"></a> Exibições do sistema – Exibições de gerenciamento dinâmico  
  
|Object|Mais Informações|  
|------------|----------------------|  
|[sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql)|[Gerenciar e monitorar a pesquisa semântica](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|[Gerenciar e monitorar a pesquisa semântica](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql)|[Gerenciar e monitorar a pesquisa semântica](manage-and-monitor-semantic-search.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar e monitorar a pesquisa semântica](manage-and-monitor-semantic-search.md)  
  
  
