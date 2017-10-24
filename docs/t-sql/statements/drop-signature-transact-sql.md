---
title: ASSINATURA de DROP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SIGNATURE
- DROP_SIGNATURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting signatures
- dropping signatures
- DROP SIGNATURE statement
- removing signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 8a1fd8c5-0e75-4b2f-9d3c-c296bed56cc7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 81823a549f608bdcddb631084904fb303a1ddc9f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-signature-transact-sql"></a>DROP SIGNATURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Descarta uma assinatura digital de um procedimento armazenado, função, gatilho ou assembly.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP [ COUNTER ] SIGNATURE FROM module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | ASYMMETRIC KEY Asym_key_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome_de_módulo*  
 É o nome de um procedimento armazenado, função, assembly ou gatilho.  
  
 CERTIFICADO *cert_name*  
 É o nome de um certificado com que o procedimento armazenado, função, assembly ou gatilho é assinado.  
  
 CHAVE ASSIMÉTRICA *Asym_key_name*  
 É o nome de uma chave assimétrica com que o procedimento armazenado, função, assembly ou gatilho é assinado.  
  
## <a name="remarks"></a>Comentários  
 As informações sobre assinaturas são visíveis na exibição do catálogo sys.crypt_properties.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER no objeto e a permissão CONTROL no certificado ou chave assimétrica. Se uma chave privada associada estiver protegida por uma senha, o usuário também precisará ter a senha.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a assinatura de certificado `HumanResourcesDP` do procedimento armazenado `HumanResources.uspUpdateEmployeeLogin`.  
  
```  
USE AdventureWorks2012;  
DROP SIGNATURE FROM HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [crypt_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [Adicionar assinatura &#40; Transact-SQL &#41;](../../t-sql/statements/add-signature-transact-sql.md)  
  
  

