---
title: osql não oferece suporte a comandos ED e !! Comandos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- ED command
- osql utility [SQL Server]
- '!! command'
ms.assetid: 7cc2852f-94e8-4292-9326-c3f1a1acd281
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fd6c1da0c11c8fa71570dbb7034c885877e22b7a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62805725"
---
# <a name="osql-no-longer-supports-the-ed-and--commands"></a>osql não oferece suporte a comandos ED e !! comandos
  O **osql** utilitário não oferece suporte a **ED** e **!!** comandos.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova as referências para o **ED** e **!!** comandos de seus scripts.  
  
 Se você quiser usar o **ED** e **!!** comandos, use o **sqlcmd** utility em vez de **osql**.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
