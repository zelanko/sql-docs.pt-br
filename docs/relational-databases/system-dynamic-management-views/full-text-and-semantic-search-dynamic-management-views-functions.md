---
title: "Exibições de gerenciamento dinâmico de pesquisa de texto completo e semântica - funções | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dynamic management objects [SQL Server], full-text search
- full-text search [SQL Server], dynamic management views
ms.assetid: 199dbd5a-29f6-4ef0-8e65-86e32c0aaa3a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4a0e0d9925f516ecbcd3fdd32d152acc866bdc8
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="full-text-and-semantic-search-dynamic-management-views---functions"></a>Exibições de gerenciamento dinâmico de pesquisa de texto completo e semântica - funções
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta seção contém as seguintes exibições e funções de gerenciamento dinâmico relacionadas à pesquisa de texto completo e pesquisa semântica.  
  
## <a name="full-text-search-dynamic-management-views-and-functions"></a>Exibições e funções de gerenciamento dinâmico de pesquisa de texto completo  
 [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
 Retorna informações sobre os catálogos de texto completo que têm alguma atividade de população em andamento no servidor.  
  
 [sys.dm_fts_fdhosts](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
 Retorna informações sobre a atividade atual do host (ou hosts) daemon do filtro da instância de servidor.  
  
 [sys.dm_fts_index_keywords](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
 Retorna informações sobre o conteúdo de um índice de texto completo da tabela especificada.  
  
 [sys.dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
 Retorna informações sobre o conteúdo no nível de documento de um índice de texto completo da tabela especificada. Uma determinada palavra-chave pode aparecer em vários documentos.  
  
 [sys.dm_fts_index_keywords_by_property](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
 Retorna todo o conteúdo relacionado a propriedade no índice de texto completo de uma determinada tabela. Isso inclui todos os dados pertencentes a qualquer propriedade registrada pela lista de propriedades de pesquisa associada àquele índice de texto completo.  
  
 sys.dm_fts_index_keywords_position_by_document  
 Retorna a posição das palavras-chave em um documento.  
  
 [sys.dm_fts_index_population](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
 Retorna informações sobre as populações de índice de texto completo que estão em andamento.  
  
 [sys.dm_fts_memory_buffers](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
 Retorna informações sobre buffers de memória pertencentes a um pool de memória específico usado como parte de um rastreamento de texto completo ou um intervalo de rastreamento de texto completo.  
  
 [sys.dm_fts_memory_pools](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
 Retorna informações sobre os pools de memória compartilhada disponíveis para o componente Full-Text Gatherer em um rastreamento de texto completo ou um intervalo de rastreamento de texto completo.  
  
 [sys.dm_fts_outstanding_batches](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
 Retorna informações sobre cada lote de indexação de texto completo.  
  
 [sys.dm_fts_parser](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)  
 Retorna o resultado final da geração de tokens após a aplicação de uma determinada combinação de separador de palavras, dicionário de sinônimos e lista de palavras irrelevantes a uma entrada de cadeia de caracteres de consulta. A saída será equivalente à saída se a cadeia de caracteres de consulta especificada foi emitida para o Mecanismo de Texto Completo.  
  
 [sys.dm_fts_population_ranges](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
 Retorna informações sobre os intervalos específicos relacionados a uma população de índice de texto completo atualmente em andamento.  
  
## <a name="semantic-search-dynamic-management-views-and-functions"></a>Exibições e funções de gerenciamento dinâmico de pesquisa semântica  
 [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
 Retorna uma linha de informações de status sobre a população do índice de similaridade de documento para cada índice de similaridade em cada tabela que tem um índice semântico associado.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [System Views &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
