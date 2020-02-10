---
title: Melhorar o desempenho de consultas de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: 0658dc74-25eb-4486-bbd6-e85c1f92c272
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96a37b1b59043079f52ca922f1ab3e7dfc9cc0ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011271"
---
# <a name="improve-the-performance-of-full-text-queries"></a>Melhorar o desempenho de consultas de texto completo
  A lista a seguir apresenta recomendações que ajudarão a melhorar o desempenho das consultas de texto completo.  
  
 O desempenho das consultas de texto completo também é influenciado por recursos de hardware, como memória, velocidade de disco, velocidade de CPU e arquitetura de computador.  
  
-   Desfragmente o índice da tabela base usando [ALTER INDEX REORGANIZE](/sql/t-sql/statements/alter-index-transact-sql).  
  
-   Reorganize o catálogo de texto completo usando [ALTER FULLTEXT CATALOG REORGANIZE](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql). Faça isso antes de testar o desempenho, pois a execução dessa instrução provoca uma mesclagem mestra dos índices de texto completo desse catálogo.  
  
-   Restrinja suas opções de colunas de chave de texto completo a uma coluna pequena. Embora haja suporte para uma coluna de 900 bytes, é recomendável usar uma coluna de chave menor em um índice de texto completo. 
  `int` e `bigint` fornecem o melhor desempenho.  
  
-   O uso de uma chave de texto completo de inteiro evita uma junção com a tabela de mapeamento **docid** . Portanto, uma chave de texto completo de inteiro melhora o desempenho de consultas consideravelmente e aprimora o desempenho de rastreamento. Outros benefícios de desempenho poderão ser obtidos se a chave de texto completo também for a chave de índice clusterizado.  
  
-   Combine vários predicados [CONTAINS](/sql/t-sql/queries/contains-transact-sql) em um único predicado CONTAINS. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode especificar uma lista de colunas na consulta CONTAINS.  
  
-   Se você só precisar de informações de classificação ou de chave de texto completo, use [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) ou [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) em vez de CONTAINS ou FREETEXT, respectivamente.  
  
-   Para limitar os resultados e melhorar o desempenho, use o parâmetro *top_n_by_rank* das funções FREETEXTTABLE e CONTAINSTABLE. *top_n_by_rank* permite que você recupere apenas as ocorrências mais relevantes. Use este parâmetro apenas se o seu cenário comercial não exige a recuperação de todos os acertos possíveis (isto é, não exige a *recuperação total*).  
  
    > [!NOTE]  
    >  A recuperação total geralmente só é necessária em cenários legais, mas pode ser menos importante do que o desempenho em cenários comerciais, como e-business.  
  
-   Verifique o plano de consulta de texto completo para assegurar que o plano de junção apropriado foi escolhido. Use uma dica de junção ou de consulta se necessário. Se um parâmetro for usado na consulta de texto completo, o valor inicial do parâmetro determinará o plano de consulta. Você pode usar a [dica de consulta](/sql/t-sql/queries/hints-transact-sql-query) OPTIMIZE FOR para forçar a consulta a ser compilada com o valor desejado. Isso ajuda a conseguir um plano de consulta determinista e melhor desempenho.  
  
-   Um número excessivo de fragmentos de índice de texto completo no índice de texto completo pode levar a uma diminuição considerável do desempenho de consulta. Para reduzir a quantidade de fragmentos, reorganize o catálogo de texto completo usando a opção REORGANIZE da instrução [ALTER FULLTEXT CATALOG](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] . Essa instrução basicamente mescla todos os fragmentos em um único fragmento maior e remove todas as entradas obsoletas do índice de texto completo.  
  
-   Na pesquisa de texto completo do , os operadores lógicos especificados em CONTAINSTABLE (AND, OR) podem ser implementados como junções SQL ou nas STVF (funções com valor de tabela de fluxo) de execução de texto completo. Em geral, as consultas que têm apenas um tipo de operadores lógicos são implementadas meramente por execução de texto completo, enquanto as consultas que combinam operadores lógicos também possuem junções SQL. A implementação de um operador lógico dentro da STVF de execução de texto completo usa algumas propriedades de índice especiais que a tornam bem mais rápida do que as junções SQL. Por isso, é recomendável que, quando possível, você forme as consultas usando um único tipo de operador lógico.  
  
-   Para aplicativos que contêm afirmações de relação seletiva, as consultas que usam predicados relacionais seletivos e predicados de texto completo não seletivos podem ter melhor desempenho quando escritas para usar o otimizador de consulta. Dessa forma, o otimizador de consulta pode decidir se poderá explorar o predicado ou a aplicação de intervalo para gerar um plano de consulta eficaz. Esta abordagem é mais simples e geralmente mais eficiente do que a indexação de dados relacionais como dados de texto completo.  
  
## <a name="related-resources"></a>Recursos relacionados  
 [Pesquisa de Texto Completo do SQL Server 2008: Operações internas e aprimoramentos](https://go.microsoft.com/fwlink/?LinkId=129544)  
  
## <a name="see-also"></a>Consulte Também  
 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql)   
 [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql)  
  
  
