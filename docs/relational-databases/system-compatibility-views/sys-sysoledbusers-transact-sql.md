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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076530"
---
# <a name="syssysoledbusers-transact-sql"></a>sys.sysoledbusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  Esta tabela do sistema [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] foi incluída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como uma exibição somente visando à compatibilidade com versões anteriores. É recomendável usar [exibições de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) em vez disso.  
  
 Contém uma linha para cada mapeamento de usuário e senha para o servidor vinculado especificado. **sysoledbusers** é armazenado no banco de dados **mestre** .  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**rmtsrvid**|**smallint**|Número de identificação de segurança do servidor.|  
|**rmtloginame**|**nvarchar (** 128 **)**|Nome do logon remoto que o **LoginSid** mapeia para o **rmtservid**vinculado.|  
|**rmtpassword**|**nvarchar (** 128 **)**|Retorna NULL.|  
|**loginsid**|**varbinary (** 85 **)**|Identificação de segurança do logon local que será mapeado.|  
|**Estado**|**smallint**|Se 1, o mapeamento deve usar as credenciais do usuário.|  
|**changeDate**|**datetime**|Data da última alteração feita nas informações do mapeamento.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;&#41;Transact-SQL](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
