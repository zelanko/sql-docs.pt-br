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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bafbc9a0e8712d0d81bed477e21f6932f3a47694
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446592"
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Registra quais logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão associados a cada conta proxy do SQL Server Agent. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|ID da conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Esse valor corresponde à coluna **proxy_id** na tabela **sysproxies** .|  
|**sid**|**varbinary (85)**|Microsoft Windows *security_identifier* para o logon do SQL Server.|  
|**principal_id**|**int**|ID do usuário ou grupo que têm permissão para usar a conta proxy de uma etapa de subsistema especificada.|  
|**sinalizadores**|**int**|Tipo de logon:<br /><br /> **0** = usuário ou grupo do Windows e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de sistema fixa<br /><br /> **2**  =  função de banco de dados **msdb**|  
  
## <a name="remarks"></a>Comentários  
 Somente os membros da função de servidor fixa **sysadmin** podem acessar essa tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [dbo.sysproxies &#40;&#41;de Transact-SQL ](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
