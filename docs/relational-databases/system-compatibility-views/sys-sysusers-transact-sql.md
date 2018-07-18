---
title: sys. sysusers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysusers
- sys.sysusers_TSQL
- sysusers_TSQL
- sysusers
dev_langs:
- TSQL
helpviewer_keywords:
- sysusers system table
- sys.sysusers compatibility view
ms.assetid: 5f0e6a8d-c983-44f6-97e9-aab5bff67d18
caps.latest.revision: 36
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0561ed37fa705f0952ae2a6e7cfd012d81364432
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38000958"
---
# <a name="syssysusers-transact-sql"></a>sys.sysusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada [!INCLUDE[msCoName](../../includes/msconame-md.md)] usuário do Windows, o grupo do Windows, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuário, ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função no banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**UID**|**smallint**|ID do usuário ID, exclusivo neste banco de dados.<br /><br /> 1 = proprietário de banco de dados<br /><br /> Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|Nome do usuário ou nome do grupo, exclusivo neste banco de dados.|  
|**sid**|**varbinary(85)**|Identificador de segurança para esta entrada.|  
|**Funções**|**varbinary(2048)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|Data em que a conta foi adicionada.|  
|**updatedate**|**datetime**|A data em que a conta foi alterada pela última vez.|  
|**altuid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
|**password**|**varbinary(256)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**gid**|**smallint**|ID do grupo ao qual este usuário pertence. Se **uid** é o mesmo que **gid**, esta entrada definirá um grupo. Estoura ou retorna NULL se o número de usuários e grupos combinados exceder 32.767.|  
|**environ**|**varchar(255)**|Reservado.|  
|**hasdbaccess**|**int**|1 = Conta tem acesso ao banco de dados.|  
|**islogin**|**int**|1 = Conta é um grupo do Windows, usuário do Windows ou usuário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conta de logon.|  
|**isntname**|**int**|1 = Conta é um grupo do Windows ou usuário do Windows.|  
|**isntgroup**|**int**|1 = Conta é um grupo do Windows.|  
|**isntuser**|**int**|1 = Conta é um usuário do Windows.|  
|**issqluser**|**int**|1 = Conta é um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**isaliased**|**int**|1 = Conta recebeu alias de outro usuário.|  
|**issqlrole**|**int**|1 = Conta é uma função de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**isapprole**|**int**|1 = Conta é uma função de aplicativo.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
