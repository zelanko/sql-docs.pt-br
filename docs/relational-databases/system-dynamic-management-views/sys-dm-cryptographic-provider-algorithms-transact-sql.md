---
title: sys. dm_cryptographic_provider_algorithms (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cryptographic_provider_algorithms_TSQL
- sys.dm_cryptographic_provider_algorithms
- sys.dm_cryptographic_provider_algorithms_TSQL
- dm_cryptographic_provider_algorithms
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_algorithms dynamic management function
ms.assetid: 8bcccb37-5cfb-4e1e-a0bb-7ff4c279fe8e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d465515d6446c16fc9186b03eafc9a287571bc5e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824667"
---
# <a name="sysdm_cryptographic_provider_algorithms-transact-sql"></a>sys.dm_cryptographic_provider_algorithms (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna os algoritmos oferecidos por um provedor de Gerenciamento Extensível de Chaves (EKM).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_cryptographic_provider_algorithms ( provider_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *provider_id*  
 Número de identificação do provedor de EKM, sem padrão.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|algorithm_id|**int**|É o número de identificação do algoritmo.|  
|algorithm_tag|**nvarchar(60)**|É a marca de identificação do algoritmo.|  
|key_type|**nvarchar(128)**|Mostra o tipo de chave. Retorna ASYMMETRIC KEY ou SYMMETRIC KEY.|  
|key_length|**int**|Indica o comprimento da chave em bits.|  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ser um membro da função de banco de dados public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte mostra as opções de provedor de um provedor com o número de identificação de `1234567`.  
  
```  
SELECT * FROM sys.dm_cryptographic_provider_algorithms(1234567);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento extensível de chaves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à segurança &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
