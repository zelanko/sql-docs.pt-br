---
title: Renomear logons que coincidem com nomes de função de servidor fixa | Microsoft Docs
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
- user-defined login names [SQL Server]
- fixed server roles [SQL Server]
- renamed logins [SQL Server]
- logins [SQL Server], names
ms.assetid: 10a1d77c-3153-474f-a6a0-969556794467
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 54223b28e681115df1b4ecf11f4fb96d13c68fd9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011935"
---
# <a name="rename-logins-matching-fixed-server-role-names"></a>Renomear logons que coincidem com nomes de funções fixas do servidor
  O Supervisor de Atualização detectou um ou mais nomes de logon definidos pelo usuário que coincidem com nomes de funções fixas do servidor. Os nomes de funções de servidor fixas são exclusivos. Renomeie o logon antes de atualizar.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
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
  
3.  Use o **sp_addlogin** procedimento de sistema para criar novos logons. Especifique o SID retornado na etapa 1 do **@sid** parâmetro para cada logon correspondente.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
