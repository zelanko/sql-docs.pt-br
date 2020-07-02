---
title: Exibições do catálogo de pesquisa de texto completo e de semântica (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- catalog views [SQL Server], full-text search
- full-text search [SQL Server], catalog views
- full-text indexes [SQL Server], catalog views
ms.assetid: b08ad2fd-e3d8-458f-96f1-678217e0f419
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 0272ab778c538b2fa8690493606a346d713fa6d5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764808"
---
# <a name="full-text-search-and-semantic-search-catalog-views-transact-sql"></a>Exibições de catálogo da pesquisa de texto completo e pesquisa semântica (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta seção descreve as exibições de catálogo que fornecem informações sobre índices de texto completo e índices semânticos.  
  
## <a name="full-text-search-catalog-views"></a>Exibições do catálogo de pesquisa de texto completo  
 [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)  
 Contém uma linha para cada catálogo de texto completo.  
  
 [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md)  
 Retorna uma linha para cada tipo de documento disponível para operações de indexação de texto completo. Cada linha representa a interface do **IFilter** que é registrada na instância do SQL Server.  
  
 [sys.fulltext_index_catalog_usages](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)  
 Retorna uma linha para cada catálogo de texto completo para referência de índice de texto completo.  
  
 [sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
 Contém uma linha para cada coluna que faz parte de um índice de texto completo.  
  
 [sys.fulltext_index_fragments](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)  
 Contém uma linha para cada fragmento de índice de texto completo em cada tabela que contém um índice de texto completo.  
  
 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
 Contém uma linha por índice de texto completo de um objeto tabular.  
  
 [sys.fulltext_languages](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)  
 Contém uma linha por idioma cujos separadores de palavras estão registrados no SQL Server. Cada linha exibe o LCID e o nome do idioma.  
  
 [sys.fulltext_stoplists](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
 Contém uma linha por lista de palavras irrelevantes de texto completo no banco de dados.  
  
 [sys.fulltext_stopwords](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
 Contém uma linha por palavra irrelevante para todas as listas de palavras irrelevantes do banco de dados.  
  
 [sys.fulltext_system_stopwords](../../relational-databases/system-catalog-views/sys-fulltext-system-stopwords-transact-sql.md)  
 Fornece acesso à lista de palavras irrelevantes do sistema.  
  
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)  
 Contém uma linha para cada propriedade de pesquisa contida por qualquer lista de propriedades de pesquisa no banco de dados atual.  
  
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
 Contém uma linha para cada lista de propriedades de pesquisa no banco de dados atual.  
  
## <a name="semantic-search-catalog-views"></a>Exibições do catálogo de pesquisa semântica  
 [sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)  
 Retorna uma linha sobre o banco de dados de estatísticas semânticas de idioma instalado na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)  
 Retorna uma linha para cada idioma cujo modelo de estatística está registrado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando um modelo de idioma está registrado, o idioma é habilitado para indexação semântica.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições e funções de gerenciamento dinâmico de pesquisa de texto completo e de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
