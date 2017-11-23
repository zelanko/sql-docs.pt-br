---
title: sys.DM cryptographic_provider_keys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys
- sys.dm_cryptographic_provider_keys
dev_langs: TSQL
helpviewer_keywords: sys.dm_cryptographic_provider_keys dynamic management function
ms.assetid: 5a8c1421-c56b-44b5-96e5-4f01782a0c7c
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b16cf946a2e963ac0421fe91ac11df6e9021ed1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmcryptographicproviderkeys-transact-sql"></a>sys.dm_cryptographic_provider_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre as chaves fornecidas por um provedor de EKM (gerenciamento de chave extensível).  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dm_cryptographic_provider_keys ( provider_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *provider_id*  
 Número de identificação do provedor de EKM, sem padrão.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**key_id**|**int**|Número de identificação da chave no provedor.|  
|**key_name**|**nvarchar(512)**|Nome da chave no provedor.|  
|**key_thumbprint**|**varbinary(32)**|Impressão digital do provedor da chave.|  
|**algorithm_id**|**int**|Número de identificação do algoritmo no provedor.|  
|**algorithm_tag**|**int**|Marca do algoritmo no provedor.|  
|**key_type**|**nchar(256)**|Tipo de chave no provedor.|  
|**comprimento_de_chave**|**int**|Comprimento da chave no provedor.|  
  
## <a name="permissions"></a>Permissões  
 Quando essa exibição for consultada, ela autenticará o contexto do usuário junto ao provedor e enumerará todas as chaves visíveis ao usuário.  
  
 Se o usuário não puder autenticar com o provedor de EKM, nenhuma informação de chave será retornada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte mostra as propriedades de chave de um provedor com o número de identificação `1234567`.  
  
```  
SELECT * FROM sys.dm_cryptographic_provider_keys(1234567);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
