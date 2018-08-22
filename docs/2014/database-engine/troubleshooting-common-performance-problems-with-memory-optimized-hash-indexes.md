---
title: Solução de problemas comuns de desempenho com índices de Hash com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1954a997-7585-4713-81fd-76d429b8d095
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 28fea2aed82e86d58264311914a341fb6ecca4fc
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394799"
---
# <a name="troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes"></a>Solucionando problemas comuns de desempenho com índices de hash com otimização de memória
  Este tópico abordará a solução de problemas e como contornar problemas comuns com índices de hash.  
  
## <a name="search-requires-a-subset-of-hash-index-key-columns"></a>A busca requer um subconjunto de colunas de chave de índice de hash  
 **Problema:** índices de Hash requerem valores para todas as colunas de chave de índice para calcular o valor de hash e localizar as linhas correspondentes na tabela de hash. Em virtude disso, se uma consulta inclui predicados de igualdade para apenas um subconjunto das chaves do índice na cláusula WHERE, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não pode usar uma busca de índice para localizar as linhas que correspondem aos predicados na cláusula WHERE.  
  
 Em contraste, índices ordenados, como os índices não clusterizados baseados em disco e os índices não clusterizados com otimização de memória, dão suporte à busca de índice em um subconjunto das colunas de chave de índice, desde que elas sejam as colunas principais do índice.  
  
 **Sintoma:** isso resulta na degradação de desempenho, como [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precisa para executar verificações de tabela completa em vez de uma busca de índice, que normalmente é uma operação mais rápida.  
  
 **Como solucionar problemas:** além da degradação do desempenho, a inspeção dos planos de consulta mostrará uma verificação em vez de uma busca de índice. Se a consulta for bem simples, a inspeção do texto da consulta e da definição de índice também mostrará se a busca requer um subconjunto das colunas de chave de índice.  
  
 Considere a seguinte tabela e consulta:  
  
```tsql  
CREATE TABLE [dbo].[od]  
(  
     o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
     CONSTRAINT PK_od PRIMARY KEY NONCLUSTERED HASH (o_id, od_id) WITH (BUCKET_COUNT = 10000)  
)  
WITH (MEMORY_OPTIMIZED = ON)  
  
 SELECT p_id  
 FROM dbo.od  
 WHERE o_id=1  
```  
  
 A tabela tem um índice de hash nas duas colunas (o_id, od_id), enquanto a consulta tem um predicado de igualdade (o_id). Como a consulta tem predicados de igualdade em apenas um subconjunto das colunas de chave de índice, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não pode executar uma operação de busca de índice usando PK_od; em vez disso, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precisa reverter para uma verificação de índice completo.  
  
 **Soluções alternativas:** há uma série de possíveis soluções alternativas. Por exemplo:  
  
-   Recrie o índice como o tipo não clusterizado em vez do hash não clusterizado. O índice não clusterizado com otimização de memória é ordenado e, portanto, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode executar uma busca de índice nas colunas principais de chave de índice. A definição de chave primária resultante para o exemplo seria `constraint PK_od primary key nonclustered`.  
  
-   Alterar a chave de índice atual para corresponder às colunas na cláusula WHERE.  
  
-   Adicionar um novo índice de hash que corresponde às colunas na cláusula WHERE da consulta. No exemplo, a definição da tabela resultante teria esta aparência:  
  
    ```tsql  
    CREATE TABLE dbo.od  
     ( o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
  
     CONSTRAINT PK_od PRIMARY KEY   
     NONCLUSTERED HASH (o_id,od_id) WITH (BUCKET_COUNT=10000),  
  
     INDEX ix_o_id NONCLUSTERED HASH (o_id) WITH (BUCKET_COUNT=10000)  
  
     ) WITH (MEMORY_OPTIMIZED=ON)  
    ```  
  
 Observe que um índice de hash com otimização de memória não apresenta o desempenho ideal quando há muitas linhas duplicadas para um valor de chave de índice específico: no exemplo, se o número de valores exclusivos para a coluna o_id fosse bem menor do que o número de linhas na tabela, o ideal não seria adicionar um índice (o_id); a melhor solução seria alterar o tipo de índice PK_od de hash para não clusterizado. Para obter mais informações, consulte [determinando o número de buckets correta para índices de Hash](../relational-databases/indexes/indexes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Índices em tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
