---
title: "Alterar a seguran&#231;a da transa&#231;&#227;o em uma sess&#227;o de espelhamento de banco de dados (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "segurança de transação [espelhamento de banco de dados do SQL Server]"
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
caps.latest.revision: 38
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 38
---
# Alterar a seguran&#231;a da transa&#231;&#227;o em uma sess&#227;o de espelhamento de banco de dados (Transact-SQL)
  A segurança da transação é o atributo que controla o modo de operação da sessão. Em qualquer momento, porém, o proprietário do banco de dados pode alterar a segurança da transação. Por padrão, o nível de segurança da transação é definido como FULL (modo de operação síncrono).  
  
 Quando a segurança da transação é desativada, a sessão é alternada para o modo de operação assíncrono, que maximiza desempenho. Se o servidor principal ficar indisponível, o espelho para, mas fica disponível em espera passiva (failover requer que o serviço seja forçado com possível perda de dados).  
  
### Para ativar a segurança da transação  
  
1.  Conecte-se ao servidor principal.  
  
2.  Emita a seguinte instrução Transact-SQL:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     em que *\<database>* é o nome do banco de dados espelhado.  
  
### Para desativar a segurança da transação  
  
1.  Conecte-se ao servidor principal.  
  
2.  Emita a seguinte instrução:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     em que *\<database>* é o banco de dados espelhado.  
  
## Consulte também  
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [Modos de operação de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  