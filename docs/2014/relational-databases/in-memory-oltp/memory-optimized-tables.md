---
title: Tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14dddf81-b502-49dc-a6b6-d18b1ae32d2b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9123bf89f75fce68a6edd8ba1becd141821fe326
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63158756"
---
# <a name="memory-optimized-tables"></a>Tabelas com otimização de memória
  O OLTP na memória do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajuda a aumentar o desempenho de aplicativos OLTP por meio de acesso a dados com otimização de memória eficiente, compilação nativa de lógica de negócios e algoritmos livres de bloqueio e trava. O recurso OLTP na memória inclui tipos de tabela e tabelas com otimização de memória, bem como compilação nativa de procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] para acesso eficiente a essas tabelas.  
  
 Para obter mais informações sobre tabelas com otimização de memória, consulte:  
  
-   [Introdução às tabelas com otimização de memória](memory-optimized-tables.md)  
  
     Detalha o que são tabelas com otimização de memória e fornece informações sobre durabilidade de dados, acesso a dados em tabelas com otimização de memória e desempenho e escalabilidade.  
  
-   [Compilação nativa de tabelas e procedimentos armazenados](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
     Detalha como tabelas com otimização de memória e procedimentos armazenados compilados nativamente são compilados para DLLs, além de fornecer considerações relacionadas sobre segurança.  
  
-   [Alterando tabelas com otimização de memória](altering-memory-optimized-tables.md)  
  
     Diretrizes para atualizar tabelas com otimização de memória (incluindo alterar colunas de tabela, índices e bucket_count).  
  
-   [Compreendendo transações em tabelas com otimização de memória](../../database-engine/understanding-transactions-on-memory-optimized-tables.md)  
  
     Esta seção fornece vários tópicos relacionados a realizar transações em tabelas com otimização de memória, incluindo níveis de isolamento de transação e transações intercontêineres.  
  
-   [Padrão de aplicativo para particionamento de tabelas com otimização de memória](application-pattern-for-partitioning-memory-optimized-tables.md)  
  
     Amostra de código detalhada que mostra como emular tabelas particionadas ao usar tabelas com otimização de memória.  
  
-   [Estatísticas para tabelas com otimização de memória](statistics-for-memory-optimized-tables.md)  
  
     Detalha como as estatísticas são compiladas para tabelas com otimização de memória e como manter e atualizar estatísticas para tabelas com otimização de memória.  
  
-   [Páginas de código de ordenações](../../database-engine/collations-and-code-pages.md)  
  
     Detalha as restrições sobre ordenações com suporte e páginas de código para tabelas com otimização de memória.  
  
-   [Tamanho da tabela e da linha em tabelas com otimização de memória](table-and-row-size-in-memory-optimized-tables.md)  
  
     Detalha o limite de 8060 bytes em linhas de tabela com otimização de memória e fornece um exemplo para calcular tamanhos de tabela e linha.  
  
-   [Um guia para processamento de consulta de tabelas com otimização de memória](a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
     Fornece uma visão geral do processamento de consulta para tabelas com otimização de memória e procedimentos armazenados compilados nativamente.  
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
