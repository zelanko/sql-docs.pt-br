---
title: "Alterar a segurança da transação em uma sessão de espelhamento de banco de dados (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 828a9d7c3bbb7ee46029bcc6bb81dab4477bcd6a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>Alterar a segurança da transação em uma sessão de espelhamento de banco de dados (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A segurança da transação é o atributo que controla o modo de operação da sessão. Em qualquer momento, porém, o proprietário do banco de dados pode alterar a segurança da transação. Por padrão, o nível de segurança da transação é definido como FULL (modo de operação síncrono).  
  
 Quando a segurança da transação é desativada, a sessão é alternada para o modo de operação assíncrono, que maximiza desempenho. Se o servidor principal ficar indisponível, o espelho para, mas fica disponível em espera passiva (failover requer que o serviço seja forçado com possível perda de dados).  
  
### <a name="to-turn-on-transaction-safety"></a>Para ativar a segurança da transação  
  
1.  Conecte-se ao servidor principal.  
  
2.  Emita a seguinte instrução Transact-SQL:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     em que *\<database>* é o nome do banco de dados espelhado.  
  
### <a name="to-turn-off-transaction-safety"></a>Para desativar a segurança da transação  
  
1.  Conecte-se ao servidor principal.  
  
2.  Emita a seguinte instrução:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     em que *\<database>* é o banco de dados espelhado.  
  
## <a name="see-also"></a>Consulte Também  
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [Modos de operação de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  
