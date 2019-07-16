---
title: sys. sysoledbusers (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: d7c8b97a04e8b9898a9d49a412c5c6e5a2aa910c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076530"
---
# <a name="syssysoledbusers-transact-sql"></a>sys.sysoledbusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  Esta tabela do sistema [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] foi incluída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como uma exibição somente visando à compatibilidade com versões anteriores. É recomendável que você use [exibições de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) em vez disso.  
  
 Contém uma linha para cada mapeamento de usuário e senha para o servidor vinculado especificado. **sysoledbusers** é armazenado em de **mestre** banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**rmtsrvid**|**smallint**|Número de identificação de segurança do servidor.|  
|**rmtloginame**|**nvarchar(** 128 **)**|Nome de logon remoto que **loginsid** mapeia para **rmtservid**.|  
|**rmtpassword**|**nvarchar(** 128 **)**|Retorna NULL.|  
|**loginsid**|**varbinary(** 85 **)**|Identificação de segurança do logon local que será mapeado.|  
|**status**|**smallint**|Se 1, o mapeamento deve usar as credenciais do usuário.|  
|**changedate**|**datetime**|Data da última alteração feita nas informações do mapeamento.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
