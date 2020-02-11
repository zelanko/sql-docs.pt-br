---
title: Alterar a segurança da transação em uma sessão de espelhamento de banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a79010a4fa59eaebfc743543799a1e83cc5e687d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62754924"
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>Alterar a segurança da transação em uma sessão de espelhamento de banco de dados (Transact-SQL)
  A segurança da transação é o atributo que controla o modo de operação da sessão. Em qualquer momento, porém, o proprietário do banco de dados pode alterar a segurança da transação. Por padrão, o nível de segurança da transação é definido como FULL (modo de operação síncrono).  
  
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
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [Modos de operação de espelhamento de banco de dados](database-mirroring-operating-modes.md)  
  
  
