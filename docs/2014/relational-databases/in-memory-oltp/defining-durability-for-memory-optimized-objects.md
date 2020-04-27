---
title: Definindo a durabilidade dos objetos com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ecf171c8c50e1f7ce1e7cdc9e86cd27ac6fe558b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63161995"
---
# <a name="defining-durability-for-memory-optimized-objects"></a>Definindo a durabilidade dos objetos com otimização de memória
  O OLTP na memória garante as propriedades ACID (total atomicidade, consistência, isolamento e total durabilidade). A durabilidade no contexto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nas tabelas com otimização de memória oferece as seguintes garantias:  
  
 Durabilidade transacional  
 Quando você confirma uma transação completamente durável que fez alterações (DDL ou DML) em uma tabela com otimização de memória, as alterações feitas em uma tabela durável com otimização de memória tornam-se permanentes.  
  
 Quando você confirma uma transação durável atrasada em uma tabela com otimização de memória, a transação se torna durável somente depois que o log de transações na memória é salvo em disco.  
  
 Durabilidade de reinicialização  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é reiniciado após uma pane ou um desligamento planejado, as tabelas duráveis com otimização de memória são instanciadas novamente para que sejam restauradas para o estado anterior ao desligamento ou à pane.  
  
 Durabilidade da falha de mídia  
 Se um disco com falha ou corrompido contiver uma ou mais cópias persistentes dos objetos duráveis com otimização de memória, o recurso de backup e restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restaurará as tabelas com otimização de memória na nova mídia.  
  
 Há duas opções de durabilidade nas tabelas com otimização de memória:  
  
 SCHEMA_ONLY (tabela não durável)  
 Essa opção assegura a durabilidade do esquema da tabela, inclusive os índices. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é reiniciado, a tabela não durável é recriada, mas começa sem nenhum dado. (Isso é diferente de uma tabela em tempdb, onde a tabela e seus dados são perdidos na reinicialização.) Um cenário típico para criar uma tabela não durável é armazenar dados transitórios, como uma tabela de preparo para um processo ETL. Uma durabilidade SCHEMA_ONLY evita o log e o ponto de verificação da transação, o que pode reduzir significativamente as operações de E/S.  
  
 SCHEMA_AND_DATA (tabela durável)  
 Essa opção fornece a durabilidade tanto do esquema quanto dos dados. O nível de durabilidade dos dados depende da transação que você confirmará, se completamente durável ou com durabilidade atrasada. Transações completamente duráveis fornecem a mesma garantia de durabilidade de dados e de esquema, semelhante a uma tabela baseada em disco. A durabilidade atrasada melhorará o desempenho, mas poderá resultar na perda potencial de dados caso haja uma falha no servidor ou um failover. (Para obter mais informações sobre a durabilidade atrasada, consulte [Controlar durabilidade atrasada](../logs/control-transaction-durability.md).)  
  
 O esquema da tabela com otimização de memória é persistente, semelhante às tabelas baseadas em disco, no grupo de arquivos primário de um banco de dados.  
  
 Os dados em tabelas duráveis com otimização de memória são salvos em pares de arquivos delta e de dados.  
  
 Os índices definidos nas tabelas com otimização de memória persistem apenas nos metadados, e não no armazenamento. As estruturas de índice são geradas como parte do carregamento das tabelas com otimização de memória.  
  
 As linhas são excluídas explicitamente por uma instrução DELETE ou indiretamente por uma instrução UPDATE. Uma operação UPDATE é executada como uma exclusão seguida por uma inserção. Quando uma linha é excluída, nenhuma alteração é feita em um arquivo de dados, mas uma nova linha, identificando a linha excluída, é acrescentada ao arquivo delta correspondente.  
  
 Durante as operações de recuperação ou restauração, o mecanismo OLTP na memória lê os arquivos delta e de dados para carregamento na memória física. O tempo de carregamento é determinado pelos seguintes fatores:  
  
-   A quantidade de dados a serem carregados.  
  
-   Largura de banda de E/S sequencial.  
  
-   Grau de paralelismo, determinado pelo número de contêineres de arquivo e núcleos de processador.  
  
-   A quantidade de registros de log na parte ativa do log que precisam ser refeitos.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
