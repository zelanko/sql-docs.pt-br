---
description: dbo.sysproxylogin (Transact-SQL)
title: dbo.sysproxylogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxylogin_TSQL
- sysproxylogin_TSQL
- dbo.sysproxylogin
- sysproxylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxylogin system table
ms.assetid: 433d33cb-bdf2-47bb-af78-2a40b7c8dfce
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 03668240a673e1e5a79fb6f9fb47b23523422c1f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547196"
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Registra quais logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão associados a cada conta proxy do SQL Server Agent. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|ID da conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Esse valor corresponde à coluna **proxy_id** na tabela **sysproxies** .|  
|**SIDs**|**varbinary(85)**|Microsoft Windows *security_identifier* para o logon do SQL Server.|  
|**principal_id**|**int**|ID do usuário ou grupo que têm permissão para usar a conta proxy de uma etapa de subsistema especificada.|  
|**sinalizadores**|**int**|Tipo de logon:<br /><br /> **0** = usuário ou grupo do Windows e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de sistema fixa<br /><br /> **2**  =  função de banco de dados **msdb**|  
  
## <a name="remarks"></a>Comentários  
 Somente os membros da função de servidor fixa **sysadmin** podem acessar essa tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [dbo.sysproxies &#40;&#41;de Transact-SQL ](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
