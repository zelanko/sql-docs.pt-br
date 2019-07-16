---
title: Consultando estendidas a procedimentos armazenados no SQL Server | Microsoft Docs
ms.custom: ''
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
ms.openlocfilehash: 33c2e4d945f4db077df843bd5622d883c719fd85
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064319"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>Consultando procedimentos armazenados estendidos no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuário autenticado pode exibir definidos atualmente procedimentos armazenados estendidos e o nome da DLL que cada um pertence executando o **sp_helpextendedproc** procedimento do sistema. Por exemplo, o exemplo a seguir retorna a DLL à qual **xp_hello** pertence:  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 Se **sp_helpextendedproc** é executado sem especificar um procedimento armazenado estendido, todos os procedimentos armazenados estendidos e seus DLLs são exibidos.  
  
> [!IMPORTANT]  
>  Serão passadas informações de retorno apenas para os procedimentos armazenados estendidos de propriedade do usuário ou para os quais o usuário tenha permissão. Somente os membros dos **sysadmin** função de servidor fixa e a **db_owner**, **db_securityadmin**e o **db_ddladmin** banco de dados fixo as funções podem exibir informações de todos os procedimentos armazenados estendidos.  
  
## <a name="see-also"></a>Consulte também  
 [sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
