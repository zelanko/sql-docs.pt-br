---
title: Objeto SqlTriggerContext | Microsoft Docs
description: No SQL Server integração CLR, a classe SqlTriggerContext fornece informações de contexto para um gatilho, incluindo o tipo de ação e colunas modificadas na operação.
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
ms.openlocfilehash: c6f11eda2ef791eb8c987af8d82149507770d47a
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809152"
---
# <a name="sqltriggercontext-object"></a>Objeto SqlTriggerContext
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  A classe **SqlTriggerContext** fornece informações de contexto sobre o gatilho. Essas informações contextuais incluem o tipo de ação que causou o acionamento do gatilho, as colunas que foram modificadas em uma operação UPDATE, e, no caso de um gatilho DDL (data definition language), uma estrutura XML **EventData** que descreve a operação de gatilho. Para obter mais informações e exemplos de como usar a classe **SqlTriggerContext** , consulte [gatilhos CLR](/dotnet/framework/data/adonet/sql/clr-triggers).  
  
 Para obter mais informações, consulte a documentação de referência da classe **Microsoft. SqlServer. Server. SqlTriggerContext** na documentação do SDK do .NET Framework.  
  
## <a name="see-also"></a>Consulte Também  
 [Gatilhos CLR](/dotnet/framework/data/adonet/sql/clr-triggers)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
