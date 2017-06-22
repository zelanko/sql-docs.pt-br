---
title: Escalabilidade | Microsoft Docs
ms.custom: 
ms.date: 08/27/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a4891c57-56bb-49f4-9bb5-f11b745279e5
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5ab43ba6b6a27fa46b5214a60063c5df3f5496f4
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="scalability"></a>Escalabilidade
  O SQL Server 2016 contém aprimoramentos de escalabilidade para o armazenamento em disco de tabelas com otimização de memória.  
  
-   **Vários threads para manter tabelas com otimização de memória**  
  
     Na versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], havia um único thread de ponto de verificação offline que verificava o log de transações em busca de alterações em tabelas com otimização de memória e que as mantinha em arquivos de ponto de verificação (como arquivos delta e de dados). Com um número maior de COREs, o thread de ponto de verificação offline único poderia ficar para trás.  
  
     No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], há vários threads simultâneos responsáveis por manter as alterações nas tabelas com otimização de memória.  
  
-   **Recuperação com multithread**  
  
     Na versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a aplicação de log como parte da operação de recuperação era single-threaded. No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a aplicação de log é multi-threaded.  
  
-   **Operação MERGE**  
  
     Agora, a operação MERGE é multi-threaded.  
  
-   **Exibições de gerenciamento dinâmico**  
  
     Houve alterações significativas em [sys.dm_db_xtp_checkpoint_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md) e [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md).  
  
 A Mesclagem Manual foi desabilitada, pois espera-se que a mesclagem multi-threaded acompanhe a carga.  
  
 O mecanismo OLTP na Memória continua a usar o grupo de arquivos com otimização de memória com base no FILESTREAM, mas o grupo de arquivos individuais é separado do FILESTREAM. Esses arquivos são totalmente gerenciados (para criação, remoção e coleta de lixo) pelo mecanismo de OLTP na Memória. Não há suporte para [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md).  
  
  

