---
title: Renomear logons que correspondem a nomes de função de servidor fixa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- user-defined login names [SQL Server]
- fixed server roles [SQL Server]
- renamed logins [SQL Server]
- logins [SQL Server], names
ms.assetid: 10a1d77c-3153-474f-a6a0-969556794467
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 296ae4d4051e79e3c5d3bc158ef3e87c9164ecd3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059091"
---
# <a name="rename-logins-matching-fixed-server-role-names"></a>Renomear logons que coincidem com nomes de funções fixas do servidor
  O Supervisor de Atualização detectou um ou mais nomes de logon definidos pelo usuário que coincidem com nomes de funções fixas do servidor. Os nomes de funções de servidor fixas são exclusivos. Renomeie o logon antes de atualizar.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Os seguintes nomes de funções de servidor fixas são exclusivos e não podem ser usados como nomes de logon definidos pelo usuário.  
  
-   **sysadmin**  
  
-   **serveradmin**  
  
-   **setupadmin**  
  
-   **securityadmin**  
  
-   **processadmin**  
  
-   **dbcreator**  
  
-   **diskadmin**  
  
-   **bulkadmin**  
  
## <a name="corrective-action"></a>Ação corretiva  
 Antes de atualizar, execute as seguintes etapas:  
  
1.  Execute esta instrução para registrar os SIDs (identificadores de segurança) dos logons:  
  
    ```  
    SELECT name, sid   
    FROM master.dbo.syslogins   
    WHERE name IN('sysadmin', 'serveradmin','setupadmin', 'securityadmin','processadmin', 'dbcreator','diskadmin','bulkadmin')  
    ```  
  
2.  Descarte os logons.  
  
3.  Use o procedimento do sistema **sp_addlogin** para criar novos logons. Especifique o SID retornado na etapa 1 no parâmetro ** \@ Sid** para cada logon correspondente.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
