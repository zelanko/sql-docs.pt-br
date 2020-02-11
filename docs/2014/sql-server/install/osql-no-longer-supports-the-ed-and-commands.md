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
manager: craigg
ms.openlocfilehash: 6ce7bfa0bbeec5c5ca83b7139f0ff28e3994021d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093722"
---
# <a name="osql-no-longer-supports-the-ed-and--commands"></a>osql não oferece suporte a comandos ED e !! comandos
  O utilitário **osql** não oferece suporte a **Ed** e **!!** comandos.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova as referências ao **Ed** e **!!** comandos de seus scripts.  
  
 Se você quiser usar o **Ed** e o **!!** comandos, use o utilitário **sqlcmd** em vez do **osql**.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
