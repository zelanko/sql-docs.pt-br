---
title: Substitua o uso do procedimento armazenado com novos procedimentos armazenados estendido xp_sqlagent_proxy_account por | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- xp_sqlagent_proxy_account
ms.assetid: 0e3cc931-6237-41dd-bf0d-0c03f4d8fff2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 320c7c719752a08f5b41531d7861646aa9ffe423
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48181156"
---
# <a name="replace-usage-of-the-xpsqlagentproxyaccount-extended-stored-procedure-with-new-stored-procedures"></a>Substituir a utilização do procedimento armazenado estendido xp_sqlagent_proxy_account por novos procedimentos armazenados
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent oferece suporte a vários proxies. Você define esses proxies usando um novo conjunto de procedimentos armazenados. Para obter mais informações sobre os novos procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte os seguintes tópicos dos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   ‘sp_add_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
-   ‘sp_delete_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
-   ‘sp_enum_login_for_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
-   ‘sp_enum_proxy_for_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
-   ‘sp_enum_sqlagent_subsystems ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
-   ‘sp_grant_proxy_to_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
-   ‘sp_grant_login_to_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
-   ‘sp_help_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
-   ‘sp_revoke_login_from_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
-   ‘sp_revoke_proxy_from_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
-   ‘sp_update_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])’  
  
> [!NOTE]  
>  Depois de atualizar para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], todas as instruções que usam o **xp_sqlagent_proxy_account** procedimento armazenado estendido não funcionará. Use **sp_xp_cmdshell_proxy_account** em vez de **xp_sqlagent_proxy_account** para definir o proxy para **xp_cmdshell**.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
