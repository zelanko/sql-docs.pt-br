---
title: Logons inativos do SQL Server 6.5 não podem ser atualizados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- passwords [SQL Server], dormant logins
- dormant logins
- logins [SQL Server], upgrading dormant logins
- identifying dormant logins
- password hashes [SQL Server]
ms.assetid: ebe18a74-0375-4df4-b894-239f8fdabb64
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7bf1bc14deea80f60692b9b25cc1f119ac69d307
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120935"
---
# <a name="dormant-sql-server-65-logins-cannot-be-upgraded"></a>Logons inativos do SQL Server 6.5 não podem ser atualizados
  O Supervisor de Atualização detectou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuja senha não pode ser atualizada diretamente para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para ativar esse logon, você deve redefinir a senha. Isso pode ser feito usando ALTER LOGIN.  
  
```  
ALTER LOGIN <login name> WITH PASSWORD = '<new password>' MUST_CHANGE  
```  
  
 A nova senha será validada de acordo com a política de complexidade de senha do seu sistema, a menos que a verificação de política seja desabilitada. Nós recomendamos que você use senhas complexas e não desabilite a verificação de política. A opção MUST_CHANGE obriga o usuário a selecionar uma senha nova. Isso não é obrigatório, mas é recomendado.  
  
 Você pode identificar logons inativos usando a seguinte consulta:  
  
```  
SELECT * FROM sysxlogins WHERE (xstatus & 2048) = 2048;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
