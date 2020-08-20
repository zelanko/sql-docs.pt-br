---
description: sys.sysoledbusers (Transact-SQL)
title: sys.sysoledbusers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysoledbusers
- sys.sysoledbusers_TSQL
- sysoledbusers
- sysoledbusers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoledbusers system table
- sys.sysoledbusers compatibility view
ms.assetid: fe924c17-9cad-4b2b-8124-1e0fd82931e3
author: rothja
ms.author: jroth
ms.openlocfilehash: 01a2683f063280800606ebd42ba9ce65a286ab82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482109"
---
# <a name="syssysoledbusers-transact-sql"></a>sys.sysoledbusers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

    
> [!IMPORTANT]  
>  Esta tabela do sistema [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] foi incluída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como uma exibição somente visando à compatibilidade com versões anteriores. É recomendável usar [exibições de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) em vez disso.  
  
 Contém uma linha para cada mapeamento de usuário e senha para o servidor vinculado especificado. **sysoledbusers** é armazenado no banco de dados **mestre** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**rmtsrvid**|**smallint**|Número de identificação de segurança do servidor.|  
|**rmtloginame**|**nvarchar (** 128 **)**|Nome do logon remoto que o **LoginSid** mapeia para o **rmtservid**vinculado.|  
|**rmtpassword**|**nvarchar (** 128 **)**|Retorna NULL.|  
|**loginsid**|**varbinary(** 85 **)**|Identificação de segurança do logon local que será mapeado.|  
|**status**|**smallint**|Se 1, o mapeamento deve usar as credenciais do usuário.|  
|**changedate**|**datetime**|Data da última alteração feita nas informações do mapeamento.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
