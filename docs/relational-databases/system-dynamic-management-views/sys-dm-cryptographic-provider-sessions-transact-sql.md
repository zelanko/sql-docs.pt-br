---
title: sys. dm_cryptographic_provider_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cryptographic_provider_sessions
- dm_cryptographic_provider_sessions_TSQL
- sys.dm_cryptographic_provider_sessions_TSQL
- dm_cryptographic_provider_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_sessions dynamic management function
ms.assetid: 9a4de02b-1a07-4850-979a-0861fddb7f9d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 63ee7a3cdc47d1464ea1cbd78d722938ddafac5b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824641"
---
# <a name="sysdm_cryptographic_provider_sessions-transact-sql"></a>sys.dm_cryptographic_provider_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre sessões abertas de um provedor criptográfico.  
 
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_cryptographic_provider_sessions(session_identifier)  
```  
  
## <a name="arguments"></a>Argumentos  
 *session_identifier*  
 Um inteiro que indica as sessões a serem retornadas.  
  
 0 = Conexão atual apenas  
  
 1 = Todas as conexões criptográficas  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|Número de identificação do provedor criptográfico.|  
|**session_handle**|**varbytes (8)**|Identificador de sessão criptográfica.|  
|**identidade**|**nvarchar(128)**|Identidade usada para autenticação com provedor criptográfico.|  
|**SPID**|**short**|SPID de ID da sessão da conexão. Para obter mais informações, consulte [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md).|  
  
## <a name="remarks"></a>Comentários  
 A exibição **Sys. dm_cryptographic_provider_sessions** é visível para o público para a conexão atual. Para exibir todas as conexões criptográficas, você deve ter a permissão **Control** Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de segurança &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Gerenciamento extensível de chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CRIAR provedor CRIPTOGRÁFICO &#40;&#41;Transact-SQL](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
