---
title: sys.syslogins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 54372511cab4cbcc3ecd7d2afe875325e105163d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62671925"
---
# <a name="syssyslogins-transact-sql"></a>sys.syslogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada conta de logon.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**sid**|**varbinary(85)**|Identificador de segurança.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|Data em que o logon foi adicionado.|  
|**updatedate**|**datetime**|Data em que o logon foi atualizado.|  
|**accdate**|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totcpu**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totio**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**spacelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**timelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resultlimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|Nome de logon do usuário.|  
|**dbname**|**sysname**|Nome do banco de dados padrão do usuário quando uma conexão é estabelecida.|  
|**password**|**nvarchar(128)**|Retorna NULL.|  
|**language**|**sysname**|Idioma padrão do usuário.|  
|**denylogin**|**int**|1 = O logon é um usuário ou grupo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que teve o acesso negado.|  
|**hasaccess**|**int**|1 = O logon teve o acesso ao servidor concedido.|  
|**isntname**|**int**|1 = O logon é um usuário ou grupo do Windows.<br /><br /> 0 = O logon é um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**isntgroup**|**int**|1 = O logon é um grupo do Windows.|  
|**isntuser**|**int**|1 = O logon é um usuário do Windows.|  
|**sysadmin**|**int**|1 = logon é um membro dos **sysadmin** função de servidor.|  
|**securityadmin**|**int**|1 = logon é um membro dos **securityadmin** função de servidor.|  
|**serveradmin**|**int**|1 = logon é um membro dos **serveradmin** função de servidor fixa.|  
|**setupadmin**|**int**|1 = logon é um membro dos **setupadmin** função de servidor fixa.|  
|**processadmin**|**int**|1 = logon é um membro dos **processadmin** função de servidor fixa.|  
|**diskadmin**|**int**|1 = logon é um membro dos **diskadmin** função de servidor fixa.|  
|**dbcreator**|**int**|1 = logon é um membro dos **dbcreator** função de servidor fixa.|  
|**bulkadmin**|**int**|1 = logon é um membro dos **bulkadmin** função de servidor fixa.|  
|**loginname**|**nvarchar(128)**|Nome de logon do usuário. Fornecido para compatibilidade com versões anteriores.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
