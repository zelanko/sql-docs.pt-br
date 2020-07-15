---
title: Criar e gerenciar objetos de armazenamento – objetos com otimização de memória
description: Saiba mais sobre os atributos de tabelas com otimização de memória e tabelas baseadas em disco. Use esses recursos para criar e gerenciar o armazenamento de objetos com otimização de memória.
ms.custom: seo-dt-2019
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 622aabe6-95c7-42cc-8768-ac2e679c5089
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f69a2d9f9601c56f8ed57a156f725c846120ddfa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723319"
---
# <a name="creating-and-managing-storage-for-memory-optimized-objects"></a>Criando e gerenciando armazenamento para objetos com otimização de memória
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  O mecanismo [!INCLUDE[hek_2](../../includes/hek-2-md.md)] é integrado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o que permite que você tenha tabelas com otimização de memória e tabelas baseadas em disco (tradicionais) no mesmo banco de dados. No entanto, a estrutura de armazenamento para tabelas com otimização de memória é diferente daquela para tabelas baseadas em disco.  
  
 O armazenamento de tabela com base em disco tem os seguintes atributos de chave:  
  
-   Mapeado para um grupo de arquivos, e o grupo de arquivos contém um ou mais arquivos.  
  
-   Cada arquivo é dividido em extensões de 8 páginas e cada página tem tamanho de 8 Kb.  
  
-   Uma extensão pode ser compartilhada entre várias tabelas, mas há mapeamento de 1 para 1 entre uma página alocada e a tabela ou índice. Em outras palavras, uma página não pode ter linhas de duas ou mais tabelas ou índices.  
  
-   Os dados são movidos para a memória (pool de buffers) conforme necessário e as páginas modificadas ou recém-criadas assincronamente são gravadas no disco, gerando principalmente E/S aleatória.  
  
 O armazenamento de tabelas com otimização de memória tem os seguintes atributos de chave:  
  
-   Todas as tabelas com otimização de memória são mapeadas para um grupo de arquivos de dados com otimização de memória. Esse grupo de arquivos usa sintaxe e semântica semelhantes às do Filestream.  
  
-   Não existem páginas e os dados são persistentes como uma linha.  
  
-   Todas as alterações em tabelas com otimização de memória são armazenadas, sendo anexadas a arquivos ativos. A leitura e a gravação de arquivos são sequenciais.  
  
-   Uma atualização é registrada como uma exclusão seguida de uma inserção. As linhas excluídas não são removidas imediatamente do armazenamento. As linhas excluídas são removidas por um processo em segundo plano chamado MERGE, com base em uma política conforme descrito em [Durabilidade de tabelas com otimização de memória](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md).  
  
-   Ao contrário das tabelas baseadas em disco, o armazenamento para tabelas com otimização de memória não é compactado. Ao migrar uma tabela baseada em disco compactada (ROW ou PAGE) para tabela com otimização de memória, você precisará levar em conta a alteração no tamanho.  
  
-   Uma tabela com otimização de memória pode ser durável ou não durável. Você precisa configurar o armazenamento de tabelas com otimização de memória duráveis.  
  
 Esta seção descreve os pares do arquivo do ponto de verificação e outros aspectos do armazenamento de dados em tabelas com otimização de memória.  
  
 Tópicos desta seção:  
  
-   [Configuração do armazenamento para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/configuring-storage-for-memory-optimized-tables.md)  
  
-   [O grupo de arquivos com otimização de memória](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
-   [Durabilidade de tabelas com otimização de memória](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)  
  
-   [Operação de ponto de verificação para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/checkpoint-operation-for-memory-optimized-tables.md)  
  
-   [Definindo a durabilidade dos objetos com otimização de memória](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)  
  
-   [Comparando o armazenamento de tabela baseado em disco com o armazenamento de tabela com otimização de memória](../../relational-databases/in-memory-oltp/comparing-disk-based-table-storage-to-memory-optimized-table-storage.md)  
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
