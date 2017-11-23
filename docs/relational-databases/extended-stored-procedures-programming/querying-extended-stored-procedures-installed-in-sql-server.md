---
title: Consultando estendida procedimentos armazenados instalados no SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5d17f27bf2d9822886c022103fae5834d8b4fddc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>Consultando procedimentos armazenados estendidos no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Em vez disso, use a integração CLR.  
  
 Um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuário autenticado pode exibir definidos atualmente procedimentos armazenados estendidos e o nome da DLL que cada um pertence executando o **sp_helpextendedproc** procedimento do sistema. Por exemplo, o exemplo a seguir retorna a DLL para o qual **xp_hello** pertence:  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 Se **sp_helpextendedproc** é executado sem especificar um procedimento armazenado estendido, todos os procedimentos armazenados estendidos e respectivas DLLs serão exibidos.  
  
> [!IMPORTANT]  
>  Serão passadas informações de retorno apenas para os procedimentos armazenados estendidos de propriedade do usuário ou para os quais o usuário tenha permissão. Somente membros do **sysadmin** função fixa de servidor e o **db_owner**, **db_securityadmin**e o **db_ddladmin** banco de dados fixo funções podem exibir informações para todos os procedimentos armazenados estendidos.  
  
## <a name="see-also"></a>Consulte também  
 [sp_helpextendedproc &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [sp_addextendedproc &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
