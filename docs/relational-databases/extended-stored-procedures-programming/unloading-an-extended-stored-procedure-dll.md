---
title: Descarregar um DLL de procedimento armazenado | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 31afe06af1285f2537a0712bdd8bd7d14e31e98f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Descarregando uma DLL de procedimento armazenado estendido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carrega uma DLL de procedimento armazenado estendido assim que é feita uma chamada para uma das funções da DLL. A DLL permanece carregada até o servidor ser desligado ou até o administrador do sistema usar a instrução DBCC para descarregá-la. Por exemplo, este comando descarrega o **xp_hello.dll**, permitindo que o administrador do sistema copiar uma versão mais recente desse arquivo para o diretório sem desligar o servidor:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DBCC nomedadll &#40; LIVRE &#41; &#40; Transact-SQL &#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  
