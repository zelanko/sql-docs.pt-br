---
title: Descarregando uma DLL de procedimento armazenado estendido | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
author: rothja
ms.author: jroth
ms.openlocfilehash: 76007876547b863f050d1e3fa494cbd8b30a5fc0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717660"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Descarregando uma DLL de procedimento armazenado estendido
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]carrega uma DLL de procedimento armazenado estendido assim que uma chamada é feita para uma das funções da dll. A DLL permanece carregada até o servidor ser desligado ou até o administrador do sistema usar a instrução DBCC para descarregá-la. Por exemplo, esse comando descarrega o **xp_hello.dll**, permitindo que o administrador do sistema Copie uma versão mais recente desse arquivo para o diretório sem desligar o servidor:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DBCC dllname &#40;FREE&#41; &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  
