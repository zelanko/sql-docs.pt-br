---
title: Objeto SqlTriggerContext | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: df384324ba16aac03a4c889cf4f3959c23374510
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874688"
---
# <a name="sqltriggercontext-object"></a>Objeto SqlTriggerContext
  A classe `SqlTriggerContext` fornece informações de contexto sobre o gatilho. Essas informações contextuais incluem o tipo de ação que causou o acionamento do gatilho, as colunas que foram modificadas em uma operação UPDATE, e, no caso de um gatilho DDL (data definition language), uma estrutura XML `EventData` que descreve a operação de gatilho. Para obter mais informações e exemplos de como usar o `SqlTriggerContext` classe, consulte [gatilhos CLR](../../database-engine/dev-guide/clr-triggers.md).  
  
 Para obter mais informações, consulte a documentação sobre referência de classe do `Microsoft.SqlServer.Server.SqlTriggerContext` no .NET Framework SDK.  
  
## <a name="see-also"></a>Consulte também  
 [Gatilhos CLR](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
