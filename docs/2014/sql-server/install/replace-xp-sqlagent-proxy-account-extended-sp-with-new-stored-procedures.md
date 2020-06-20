---
title: Substituir o uso da xp_sqlagent_proxy_account procedimento armazenado estendido por novos procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- xp_sqlagent_proxy_account
ms.assetid: 0e3cc931-6237-41dd-bf0d-0c03f4d8fff2
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 46de12faa52fae61e1f11758f40e1ec8242faca1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011864"
---
# <a name="replace-usage-of-the-xp_sqlagent_proxy_account-extended-stored-procedure-with-new-stored-procedures"></a>Substituir a utilização do procedimento armazenado estendido xp_sqlagent_proxy_account por novos procedimentos armazenados
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
>  Depois de atualizar para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o, todas as instruções que usam o procedimento armazenado estendido **xp_sqlagent_proxy_account** não funcionarão. Use **sp_xp_cmdshell_proxy_account** em vez de **xp_sqlagent_proxy_account** para definir o proxy para **xp_cmdshell**.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
