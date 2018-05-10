---
title: Configurar um banco de dados espelho para usar a propriedade confiável (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: high-availability
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TRUSTWORTHY database option
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 6993b076-78ef-453e-b0ea-e341b8e5ee3e
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 459c0f0589ada677bd21419b965d589b43d5771b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql"></a>Configurar um banco de dados espelho para usar a propriedade confiável (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando é feito backup de um banco de dados, a propriedade TRUSTWORTHY do banco de dados é definida como OFF. Portanto, em um novo banco de dados espelho, TRUSTWORTHY está sempre OFF. Se o banco de dados precisar estar confiável após um failover, serão necessárias etapas adicionais de instalação após o início do espelhamento.  
  
> [!NOTE]  
>  Para obter informações sobre essa propriedade de banco de dados, veja [propriedade TRUSTWORTHY do banco de dados](../../relational-databases/security/trustworthy-database-property.md).  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="to-setup-a-mirror-database-to-use-the-trustworthy-property"></a>Para configurar um banco de dados espelho para usar a Propriedade Trustworthy  
  
1.  Na instância de servidor principal, verifique se o banco de dados principal está com a propriedade Trustworthy ativada.  
  
    ```  
    SELECT name, database_id, is_trustworthy_on FROM sys.databases   
    ```  
  
     Para obter mais informações, veja [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
2.  Depois de iniciar o espelhamento, verifique se o banco de dados é atualmente o banco de dados principal, se a sessão está usando um modo operacional síncrono e se a sessão já está sincronizada.  
  
    ```  
    SELECT database_id, mirroring_role, mirroring_safety_level_desc, mirroring_state_desc FROM sys.database_mirroring  
    ```  
  
     Para obter mais informações, veja [sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md).  
  
3.  Quando a sessão de espelhamento está sincronizada, faça o failover manualmente para o banco de dados espelho.  
  
     Isto pode ser feito no SQL Server Management Studio ou usando o Transact-SQL:  
  
    -   [Executar failover manualmente de uma sessão de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [Executar failover manualmente em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-transact-sql.md)  
  
4.  Ative a propriedade de banco de dados confiável que usa o seguinte comando ALTER DATABASE:  
  
    ```  
    ALTER DATABASE <database_name> SET TRUSTWORTHY ON  
    ```  
  
     Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
5.  Opcionalmente, faça novamente o failover manualmente para voltar ao principal original.  
  
6.  Opcionalmente, alterne para o modo assíncrono, de alto desempenho, definindo SAFETY como OFF e assegurando que WITNESS também esteja definido como OFF.  
  
     No Transact-SQL:  
  
    -   [Alterar a segurança da transação em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)  
  
    -   [Remover a testemunha de uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
     No SQL Server Management Studio:  
  
    -   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="see-also"></a>Consulte Também  
 [propriedade TRUSTWORTHY do banco de dados](../../relational-databases/security/trustworthy-database-property.md)   
 [Configurar um banco de dados espelho criptografado](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
  
