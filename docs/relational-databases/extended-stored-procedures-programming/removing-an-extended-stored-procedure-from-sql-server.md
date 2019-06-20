---
title: Remover um procedimento armazenado a partir do SQL Server | Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: f04a0baa52eff0ac5742769e9eb6bfd7bfc246c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62742194"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Removendo um procedimento armazenado estendido do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 Para descartar cada função de procedimento armazenado estendido em uma definida pelo usuário procedimento armazenado estendido DLL, uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administrador do sistema deve executar o **sp_dropextendedproc** especificando o nome do procedimento armazenado do sistema a função e o nome da DLL em que reside essa função. Por exemplo, este comando remove a função **xp_hello**, localizado em uma DLL chamada xp_hello, de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **sp_dropextendedproc** não descarta procedimentos armazenados estendido de sistema. Em vez disso, o administrador do sistema deve negar a permissão EXECUTE no procedimento armazenado estendido para o **pública** função.  
  
## <a name="see-also"></a>Consulte também  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
