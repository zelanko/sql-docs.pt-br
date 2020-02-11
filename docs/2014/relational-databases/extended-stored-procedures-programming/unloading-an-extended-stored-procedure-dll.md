---
title: Descarregando uma DLL de procedimento armazenado estendido | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2772c8d6470f9ad6eb5e8b7cadb6dedd136bd48b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63137579"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Descarregando uma DLL de procedimento armazenado estendido
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Em vez disso, use a integração CLR.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carrega uma DLL de procedimento armazenado estendido assim que uma chamada é feita para uma das funções da dll. A DLL permanece carregada até o servidor ser desligado ou até o administrador do sistema usar a instrução DBCC para descarregá-la. Por exemplo, esse comando descarrega o **xp_hello. dll**, permitindo que o administrador do sistema Copie uma versão mais recente desse arquivo para o diretório sem desligar o servidor:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DBCC DllName &#40;gratuito&#41; &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dllname-free-transact-sql)  
  
  
