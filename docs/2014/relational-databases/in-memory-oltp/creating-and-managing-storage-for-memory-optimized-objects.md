---
title: Criando e gerenciando armazenamento para objetos com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 622aabe6-95c7-42cc-8768-ac2e679c5089
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1d6bb42e4b35a74ef2bd6eefb85ea81b0ed18e40
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63073841"
---
# <a name="creating-and-managing-storage-for-memory-optimized-objects"></a>Criando e gerenciando armazenamento para objetos com otimização de memória
  O mecanismo [!INCLUDE[hek_2](../../includes/hek-2-md.md)] é integrado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o que permite que você tenha tabelas com otimização de memória e tabelas baseadas em disco (tradicionais) no mesmo banco de dados. No entanto, a estrutura de armazenamento para tabelas com otimização de memória é diferente daquela para tabelas baseadas em disco.  
  
 O armazenamento de tabela com base em disco tem os seguintes atributos de chave:  
  
-   Mapeado para um grupo de arquivos, e o grupo de arquivos contém um ou mais arquivos.  
  
-   Cada arquivo é dividido em extensões de 8 páginas e cada página tem tamanho de 8 Kb.  
  
-   Uma extensão pode ser compartilhada entre várias tabelas, mas há mapeamento de 1 para 1 entre uma página alocada e a tabela ou índice. Em outras palavras, uma página não pode ter linhas de duas ou mais tabelas ou índices.  
  
-   Os dados são movidos para a memória (pool de buffers) conforme necessário e as páginas modificadas ou recém-criadas assincronamente são gravadas no disco, gerando principalmente E/S aleatória.  
  
 O armazenamento de tabelas com otimização de memória tem os seguintes atributos de chave:  
  
-   Todas as tabelas com otimização de memória são mapeadas para um grupo de arquivos com otimização de memória. Esse grupo de arquivos é criado usando o grupo de arquivos FILESTREAM.  
  
-   Não existem páginas e os dados são persistentes como uma linha.  
  
-   Todas as alterações em tabelas com otimização de memória são armazenadas, sendo anexadas a arquivos ativos. A leitura e a gravação de arquivos são sequenciais.  
  
-   Uma atualização é registrada como uma exclusão seguida de uma inserção. As linhas excluídas não são removidas imediatamente do armazenamento. As linhas excluídas são removidas por um processo em segundo plano chamado MERGE, com base em uma política conforme descrito em [Durabilidade de tabelas com otimização de memória](memory-optimized-tables.md).  
  
-   Ao contrário das tabelas baseadas em disco, o armazenamento para tabelas com otimização de memória não é compactado. Ao migrar uma tabela baseada em disco compactada (ROW ou PAGE) para tabela com otimização de memória, você precisará levar em conta a alteração no tamanho.  
  
-   Uma tabela com otimização de memória pode ser durável ou não durável. Você só precisa configurar o armazenamento para as tabelas duráveis de otimização de memória.  
  
 Esta seção descreve os pares do arquivo do ponto de verificação e outros aspectos do armazenamento de dados em tabelas com otimização de memória.  
  
 Tópicos desta seção:  
  
-   [Configuração do armazenamento para tabelas com otimização de memória](configuring-storage-for-memory-optimized-tables.md)  
  
-   [O grupo de arquivos com otimização de memória](the-memory-optimized-filegroup.md)  
  
-   [Durabilidade de tabelas com otimização de memória](memory-optimized-tables.md)  
  
-   [Operação de ponto de verificação para tabelas com otimização de memória](checkpoint-operation-for-memory-optimized-tables.md)  
  
-   [Definindo a durabilidade dos objetos com otimização de memória](defining-durability-for-memory-optimized-objects.md)  
  
-   [Comparando o armazenamento de tabela baseado em disco com o armazenamento de tabela com otimização de memória](comparing-disk-based-table-storage-to-memory-optimized-table-storage.md)  
  
-   [Monitorando e solucionando problemas de mesclagem de pares de arquivos delta e de dados](../../database-engine/monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs.md)  
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
