---
title: Índices de hash | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f4bdc9c1-7922-4fac-8183-d11ec58fec4e
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 3da74688d6a2f65b191788ab9ecd2394bcca8597
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020768"
---
# <a name="hash-indexes"></a>Índices de hash
  Os índices são usados como pontos de entrada para tabelas com otimização de memória. A leitura das linhas de uma tabela requer um índice para localizar os dados na memória.  
  
 Um índice de hash consiste em uma coleção de buckets organizados em uma matriz. Uma função de hash mapeia chaves de índice para buckets correspondentes no índice de hash. A figura a seguir mostra três chaves de índice mapeadas para três buckets diferentes no índice de hash. Para fins ilustrativos, o nome da função de hash é f(x).  
  
 ![Chaves de índice mapeadas para buckets diferentes. ] (../../2014/database-engine/media/hekaton-tables-2.gif "Chaves de índice mapeadas para buckets diferentes.")  
  
 A função de hash usada para índices de hash tem as seguintes características:  
  
-   O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem uma função de hash que é usada para todos os índices de hash.  
  
-   A função de hash é determinística. A mesma chave de índice sempre é mapeada para o mesmo bucket no índice de hash.  
  
-   Várias chaves de índice podem ser mapeadas para o mesmo bucket de hash.  
  
-   A função de hash é equilibrada, o que significa que a distribuição de valores de chave do índice sobre buckets de hash geralmente segue uma distribuição de Poisson.  
  
     A distribuição de Poisson não é uma distribuição uniforme. Os valores de chave de índice não são distribuídos uniformemente nos buckets de hash. Por exemplo, uma distribuição de Poisson de chaves de índice distintas *n* nos buckets de hash *n* resulta em aproximadamente um terço de buckets vazios, um terço de buckets que contêm uma chave de índice e o outro terço contendo duas chaves de índice. Um número pequeno de buckets conterá mais de duas chaves.  
  
 Se duas chaves de índice forem mapeadas para o mesmo bucket de hash, haverá uma colisão de hash. Um número grande de colisões de hash pode afetar o desempenho das operações de leitura.  
  
 A estrutura de índice de hash na memória consiste em uma matriz de ponteiros de memória. Cada bucket é mapeado para um deslocamento nesta matriz. Cada bucket na matriz aponta para a primeira linha desse bucket de hash. Cada linha no bucket aponta para a próxima linha, resultando em uma cadeia de linhas para cada bucket de hash, conforme ilustrado na figura a seguir.  
  
 ![A estrutura de índice de hash na memória. ] (../../2014/database-engine/media/hekaton-tables-3.gif "a estrutura de índice de hash na memória.")  
  
 A figura tem três buckets com linhas. O segundo bucket na parte superior contém as três linhas vermelhas. O quarto bucket contém uma única linha azul. O bucket inferior contém as duas linhas verdes. Essas versões podem ser diferentes e estarem na mesma linha.  
  
 Para obter mais informações sobre índices para tabelas com otimização de memória, consulte [Guidelines for Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
## <a name="see-also"></a>Consulte também  
 [Índices em tabelas com otimização de memória](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  