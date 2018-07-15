---
title: Remover referências a procedimentos armazenados substituídos do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- undocumented system stored procedures [SQL Server]
- system stored procedures [SQL Server]
ms.assetid: 487d24fc-41d5-495e-843c-0ac974ec472f
caps.latest.revision: 20
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5a588f8ec25301d3c8a4343e6c7f0d77eebdfe75
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187573"
---
# <a name="remove-references-to-deprecated-system-stored-procedures"></a>Remover referências a procedimentos armazenados do sistema obsoletos
  O Supervisor de Atualização detectou instruções que fazem referência a procedimentos armazenados do sistema não documentados e a procedimentos armazenados estendidos que não estão mais disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As instruções que fizerem referência a esses objetos falharão. Não use objetos ou APIs do sistema não documentados, pois a funcionalidade pode ser alterada ou removida sem notificação em uma versão futura.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
  
### <a name="documented-system-stored-procedures"></a>Procedimentos armazenados do sistema documentados  
 Os seguintes procedimentos armazenados do sistema documentados foram removidos:  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
### <a name="undocumented-system-stored-procedures"></a>Procedimentos armazenados do sistema não documentados  
 Os seguintes procedimentos armazenados do sistema não documentados e procedimentos estendidos armazenados foram removidos:  
  
-   sp_articlesynctranprocs  
  
-   sp_diskdefault  
  
-   sp_EventLog  
  
-   sp_GetMBCSCharLen  
  
-   sp_helplog  
  
-   sp_helpsql  
  
-   sp_IsMBCSLeadByte  
  
-   sp_lock2  
  
-   sp_MSget_current_activity  
  
-   sp_MSset_current_activity  
  
-   sp_MSobjessearch  
  
-   xp_enum_ActiveScriptEngines  
  
-   xp_eventlog  
  
-   xp_GetAdminGroupName  
  
-   xp_GetFileDetails  
  
-   xp_GetLocalSystemAccountName  
  
-   xp_IsNTAdmin  
  
-   xp_MSLocalSystem  
  
-   xp_MSnt2000  
  
-   xp_MSplatform  
  
-   xp_SetSecurity  
  
-   xp_varbintohexstr  
  
## <a name="corrective-action"></a>Ação corretiva  
  
### <a name="documented-system-stored-procedures"></a>Procedimentos armazenados do sistema documentados  
 Modifique seus aplicativos de acordo com a tabela a seguir:  
  
|Em vez de|Faça isto|  
|----------------|-------------|  
|sp_addalias|Substitua aliases por uma combinação de contas de usuário e funções de banco de dados. Para obter mais informações, consulte "CREATE USER (Transact-SQL)" e "CREATE ROLE (Transact-SQL)" nos Manuais Online do SQL Server. Remova aliases dos bancos de dados atualizados usando sp_dropalias.|  
|sp_addgroupsp_changegroup<br /><br /> sp_dropgroup<br /><br /> sp_helpgroup|Use funções. Para obter mais informações, consulte "Funções no nível de servidor" e "Funções no nível de banco de dados" nos Manuais Online do SQL Server.|  
  
### <a name="undocmented-system-stored-procedures"></a>Procedimentos armazenados do sistema Undocmented  
 Você pode criar procedimentos armazenados CLR com funcionalidade equivalente para substituir procedimentos armazenados do sistema não documentados. Para obter mais informações, consulte o tópico ‘Procedimentos armazenados CLR’ nos Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
