---
title: sys. syslogins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syslogins_TSQL
- syslogins
- sys.syslogins
- sys.syslogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syslogins compatibility view
- syslogins system table
ms.assetid: 4cb34f17-a4bb-469f-a218-71f074e6308f
caps.latest.revision: 41
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 924ae2b530c719085e21d7b045e4a872255b3009
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="syssyslogins-transact-sql"></a>sys.syslogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada conta de logon.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**sid**|**varbinary(85)**|Identificador de segurança.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|Data em que o logon foi adicionado.|  
|**updatedate**|**datetime**|Data em que o logon foi atualizado.|  
|**accdate**|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totcpu**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totio**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**spacelimit**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**timelimit**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resultlimit**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|Nome de logon do usuário.|  
|**dbname**|**sysname**|Nome do banco de dados padrão do usuário quando uma conexão é estabelecida.|  
|**password**|**nvarchar(128)**|Retorna NULL.|  
|**language**|**sysname**|Idioma padrão do usuário.|  
|**denylogin**|**Int**|1 = O logon é um usuário ou grupo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que teve o acesso negado.|  
|**hasaccess**|**Int**|1 = O logon teve o acesso ao servidor concedido.|  
|**isntname**|**Int**|1 = O logon é um usuário ou grupo do Windows.<br /><br /> 0 = O logon é um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**isntgroup**|**Int**|1 = O logon é um grupo do Windows.|  
|**isntuser**|**Int**|1 = O logon é um usuário do Windows.|  
|**sysadmin**|**Int**|1 = logon é um membro do **sysadmin** função de servidor.|  
|**securityadmin**|**Int**|1 = logon é um membro do **securityadmin** função de servidor.|  
|**serveradmin**|**Int**|1 = logon é um membro do **serveradmin** função de servidor fixa.|  
|**setupadmin**|**Int**|1 = logon é um membro do **setupadmin** função de servidor fixa.|  
|**processadmin**|**Int**|1 = logon é um membro do **processadmin** função de servidor fixa.|  
|**diskadmin**|**Int**|1 = logon é um membro do **diskadmin** função de servidor fixa.|  
|**dbcreator**|**Int**|1 = logon é um membro do **dbcreator** função de servidor fixa.|  
|**bulkadmin**|**Int**|1 = logon é um membro do **bulkadmin** função de servidor fixa.|  
|**loginname**|**nvarchar(128)**|Nome de logon do usuário. Fornecido para compatibilidade com versões anteriores.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
