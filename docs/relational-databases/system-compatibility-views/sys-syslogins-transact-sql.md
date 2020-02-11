---
title: sys. syslogins (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 5745d3f98741d4a414c7bb69d8f9865258d47e34
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020011"
---
# <a name="syssyslogins-transact-sql"></a>sys.syslogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada conta de logon.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**SIDs**|**varbinary(85)**|Identificador de segurança.|  
|**Estado**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**CreateDate**|**datetime**|Data em que o logon foi adicionado.|  
|**updateDate**|**datetime**|Data em que o logon foi atualizado.|  
|**accdate**|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totcpu**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totio**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**spacelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**limite de**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resultlimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|Nome de logon do usuário.|  
|**NomeDoBancoDeDados**|**sysname**|Nome do banco de dados padrão do usuário quando uma conexão é estabelecida.|  
|**password**|**nvarchar(128)**|Retorna NULL.|  
|**linguagem**|**sysname**|Idioma padrão do usuário.|  
|**denylogin**|**int**|1 = O logon é um usuário ou grupo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que teve o acesso negado.|  
|**hasaccess**|**int**|1 = O logon teve o acesso ao servidor concedido.|  
|**isntname**|**int**|1 = O logon é um usuário ou grupo do Windows.<br /><br /> 0 = O logon é um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**isntgroup**|**int**|1 = O logon é um grupo do Windows.|  
|**isntuser**|**int**|1 = O logon é um usuário do Windows.|  
|**sysadmin**|**int**|1 = o logon é um membro da função de servidor **sysadmin** .|  
|**securityadmin**|**int**|1 = o logon é um membro da função de servidor **securityadmin** .|  
|**ServerAdmin**|**int**|1 = o logon é um membro da função de servidor fixa **ServerAdmin** .|  
|**setupadmin**|**int**|1 = o logon é um membro da função de servidor fixa **setupadmin** .|  
|**processadmin**|**int**|1 = o logon é um membro da função de servidor fixa **processadmin** .|  
|**diskadmin**|**int**|1 = o logon é um membro da função de servidor fixa **diskadmin** .|  
|**dbcreator**|**int**|1 = o logon é um membro da função de servidor fixa **dbcreator** .|  
|**bulkadmin**|**int**|1 = o logon é um membro da função de servidor fixa **bulkadmin** .|  
|**LoginName**|**nvarchar(128)**|Nome de logon do usuário. Fornecido para compatibilidade com versões anteriores.|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;&#41;Transact-SQL](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
