---
title: Remover um procedimento armazenado a partir do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f1e60be2d8075c676a74539d8add407a2b7e8ab5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130765"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Removendo um procedimento armazenado estendido do SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 Para descartar cada função de procedimento armazenado estendido em uma definida pelo usuário procedimento armazenado estendido DLL, uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administrador do sistema deve executar o **sp_dropextendedproc** especificando o nome do procedimento armazenado do sistema a função e o nome da DLL em que reside essa função. Por exemplo, este comando remove a função **xp_hello**, localizado em uma DLL chamada xp_hello.dll, do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **sp_dropextendedproc** não descarta procedimentos armazenados estendido de sistema. Em vez disso, o administrador do sistema deve negar a permissão EXECUTE no procedimento armazenado estendido para o **pública** função.  
  
## <a name="see-also"></a>Consulte também  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
