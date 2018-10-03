---
title: Objeto SqlTriggerContext | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7eff223dc255d5a44706e7b97f73963863428ae8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47661687"
---
# <a name="sqltriggercontext-object"></a>Objeto SqlTriggerContext
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A classe **SqlTriggerContext** fornece informações de contexto sobre o gatilho. Essas informações contextuais incluem o tipo de ação que causou o acionamento do gatilho, as colunas que foram modificadas em uma operação UPDATE, e, no caso de um gatilho DDL (data definition language), uma estrutura XML **EventData** que descreve a operação de gatilho. Para obter mais informações e exemplos de como usar o **SqlTriggerContext** classe, consulte [gatilhos CLR](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c).  
  
 Para obter mais informações, consulte a documentação sobre referência de classe **Microsoft.SqlServer.Server.SqlTriggerContext** no SDK do .NET Framework.  
  
## <a name="see-also"></a>Consulte também  
 [Gatilhos CLR](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
