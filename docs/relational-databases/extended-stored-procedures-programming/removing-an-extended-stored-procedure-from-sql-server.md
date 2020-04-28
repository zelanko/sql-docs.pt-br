---
title: Removendo um procedimento armazenado estendido
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: ec61cf630d606977689d3fb3763cce8bd8b705c8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74095432"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Removendo um procedimento armazenado estendido do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 Para descartar cada função de procedimento armazenado estendido em uma DLL de procedimento armazenado estendido definida pelo usuário, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administrador do sistema deve executar o procedimento armazenado do sistema **sp_dropextendedproc** , especificando o nome da função e o nome da dll na qual a função reside. Por exemplo, esse comando Remove a função **xp_hello**, localizada em uma DLL chamada xp_hello. dll, de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 A [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]partir do, **sp_dropextendedproc** não remove os procedimentos armazenados estendidos do sistema. Em vez disso, o administrador do sistema deve negar a permissão EXECUTE no procedimento armazenado estendido para a função **pública** .  
  
## <a name="see-also"></a>Consulte Também  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
