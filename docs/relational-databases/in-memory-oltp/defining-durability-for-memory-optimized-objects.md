---
title: "Definindo a durabilidade dos objetos com otimização de memória | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d4f8bab5cfa0cc83737bb5736dfe4dcac84b8c13
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="defining-durability-for-memory-optimized-objects"></a>Definindo a durabilidade dos objetos com otimização de memória
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Há duas opções de durabilidade nas tabelas com otimização de memória:  
  
 SCHEMA_AND_DATA (padrão)  
 Essa opção fornece a durabilidade tanto do esquema quanto dos dados. O nível de durabilidade dos dados depende da transação que você confirmará, se completamente durável ou com durabilidade atrasada. Transações completamente duráveis fornecem a mesma garantia de durabilidade de dados e de esquema, semelhante a uma tabela baseada em disco. A durabilidade atrasada melhorará o desempenho, mas poderá resultar na perda potencial de dados caso haja uma falha no servidor ou um failover. (Para obter mais informações sobre a durabilidade atrasada, consulte [Controlar durabilidade atrasada](../../relational-databases/logs/control-transaction-durability.md).)  
  
 SCHEMA_ONLY  
 Essa opção assegura a durabilidade do esquema da tabela. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é reiniciado ou uma reconfiguração ocorre em um Banco de Dados SQL do Azure, o esquema da tabela persiste, mas os dados na tabela são perdidos. (Isso é diferente de uma tabela em tempdb, onde a tabela e seus dados são perdidos na reinicialização.) Um cenário típico para criar uma tabela não durável é armazenar dados transitórios, como uma tabela de preparo para um processo ETL. Uma durabilidade SCHEMA_ONLY evita o log e o ponto de verificação da transação, o que pode reduzir significativamente as operações de E/S.  
  
 Ao usar as tabelas SCHEMA_AND_DATA padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece as mesmas garantias de durabilidade quanto às tabelas baseadas em disco:  
  
 Durabilidade transacional  
 Quando você confirma uma transação completamente durável que fez alterações (DDL ou DML) em uma tabela com otimização de memória, as alterações feitas em uma tabela durável com otimização de memória tornam-se permanentes.  
  
 Quando você confirma uma transação durável atrasada em uma tabela com otimização de memória, a transação se torna durável somente depois que o log de transações na memória é salvo em disco. (Para obter mais informações sobre a durabilidade atrasada, consulte [Controlar durabilidade atrasada](../../relational-databases/logs/control-transaction-durability.md).)  
  
 Durabilidade de reinicialização  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é reiniciado após uma pane ou um desligamento planejado, as tabelas duráveis com otimização de memória são instanciadas novamente para que sejam restauradas para o estado anterior ao desligamento ou à pane.  
  
 Durabilidade da falha de mídia  
 Se um disco com falha ou corrompido contiver uma ou mais cópias persistentes dos objetos duráveis com otimização de memória, o recurso de backup e restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restaurará as tabelas com otimização de memória na nova mídia.  
  
## <a name="see-also"></a>Consulte também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
