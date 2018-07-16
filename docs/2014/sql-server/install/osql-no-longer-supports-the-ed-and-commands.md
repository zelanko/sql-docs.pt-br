---
title: osql não oferece suporte a comandos ED e!! comandos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ED command
- osql utility [SQL Server]
- '!! command'
ms.assetid: 7cc2852f-94e8-4292-9326-c3f1a1acd281
caps.latest.revision: 13
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cea117423d097fc63441c9bd82a33b4cc3c2e910
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243988"
---
# <a name="osql-no-longer-supports-the-ed-and--commands"></a>osql não oferece suporte a comandos ED e!! comandos
  O **osql** utilitário não oferece suporte a **ED** e **!!** comandos.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova as referências para o **ED** e **!!** comandos de seus scripts.  
  
 Se você quiser usar o **ED** e **!!** comandos, use o **sqlcmd** utility em vez de **osql**.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
