---
title: osql não oferece suporte a comandos ED e !! comandos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- ED command
- osql utility [SQL Server]
- '!! command'
ms.assetid: 7cc2852f-94e8-4292-9326-c3f1a1acd281
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1ad92a32c47002c8f56e56a5b3695d42d3bdd671
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012065"
---
# <a name="osql-no-longer-supports-the-ed-and--commands"></a>osql não oferece suporte a comandos ED e !! comandos
  O utilitário **osql** não oferece suporte a **Ed** e **!!** comandos.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova as referências ao **Ed** e **!!** comandos de seus scripts.  
  
 Se você quiser usar o **Ed** e o **!!** comandos, use o utilitário **sqlcmd** em vez do **osql**.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
