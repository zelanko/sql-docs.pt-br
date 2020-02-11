---
title: Consultando procedimentos armazenados estendidos instalados no SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9f62c0dea02ee4c6f9bccda0dfaf7e7932c1dab7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62511929"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>Consultando procedimentos armazenados estendidos no SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Em vez disso, use a integração CLR.  
  
 Um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuário autenticado pode exibir os procedimentos armazenados estendidos definidos no momento e o nome da dll à qual cada um pertence executando o procedimento do sistema **sp_helpextendedproc** . Por exemplo, o exemplo a seguir retorna a DLL à qual **xp_hello** pertence:  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 Se **sp_helpextendedproc** for executado sem especificar um procedimento armazenado estendido, todos os procedimentos armazenados estendidos e suas DLLs serão exibidos.  
  
> [!IMPORTANT]  
>  Serão passadas informações de retorno apenas para os procedimentos armazenados estendidos de propriedade do usuário ou para os quais o usuário tenha permissão. Somente os membros da função de servidor fixa **sysadmin** e o **db_owner**, **db_securityadmin**e as **db_ddladmin** funções de banco de dados fixas podem exibir informações de todos os procedimentos armazenados estendidos.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_helpextendedproc](/sql/relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_addextendedproc](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
