---
title: Removendo um procedimento armazenado estendido de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: bcb58ac180861641803147d1dfea621bd52df9a6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62512021"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Removendo um procedimento armazenado estendido do SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 Para descartar cada função de procedimento armazenado estendido em uma DLL de procedimento armazenado estendido definida pelo usuário, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administrador do sistema deve executar o procedimento armazenado do sistema **sp_dropextendedproc** , especificando o nome da função e o nome da dll na qual a função reside. Por exemplo, esse comando Remove a função **xp_hello**, localizada em uma DLL chamada xp_hello. dll, de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 A [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]partir do, **sp_dropextendedproc** não remove os procedimentos armazenados estendidos do sistema. Em vez disso, o administrador do sistema deve negar a permissão EXECUTE no procedimento armazenado estendido para a função **pública** .  
  
## <a name="see-also"></a>Consulte Também  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
