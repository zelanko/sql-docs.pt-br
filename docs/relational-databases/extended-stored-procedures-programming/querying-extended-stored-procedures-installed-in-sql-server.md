---
title: Consultando procedimentos armazenados estendidos
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 8413f071cfb36f5cad9130d3e2b56327d9b3bf45
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758093"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>Consultando procedimentos armazenados estendidos no SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuário autenticado pode exibir os procedimentos armazenados estendidos definidos no momento e o nome da dll à qual cada um pertence executando o procedimento do sistema **sp_helpextendedproc** . Por exemplo, o exemplo a seguir retorna a DLL à qual **xp_hello** pertence:  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 Se **sp_helpextendedproc** for executado sem especificar um procedimento armazenado estendido, todos os procedimentos armazenados estendidos e suas DLLs serão exibidos.  
  
> [!IMPORTANT]  
>  Serão passadas informações de retorno apenas para os procedimentos armazenados estendidos de propriedade do usuário ou para os quais o usuário tenha permissão. Somente os membros da função de servidor fixa **sysadmin** e o **db_owner**, **db_securityadmin**e as **db_ddladmin** funções de banco de dados fixas podem exibir informações de todos os procedimentos armazenados estendidos.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_helpextendedproc](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addextendedproc](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
