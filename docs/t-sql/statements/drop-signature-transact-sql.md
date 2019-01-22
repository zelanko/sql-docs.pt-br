---
title: DROP SIGNATURE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a7def68fb093f056569836a3cbdad5f71b3fbd2f
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54327687"
---
# <a name="drop-signature-transact-sql"></a>DROP SIGNATURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Descarta uma assinatura digital de um procedimento armazenado, função, gatilho ou assembly.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP [ COUNTER ] SIGNATURE FROM module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | ASYMMETRIC KEY Asym_key_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *module_name*  
 É o nome de um procedimento armazenado, função, assembly ou gatilho.  
  
 CERTIFICATE *cert_name*  
 É o nome de um certificado com que o procedimento armazenado, função, assembly ou gatilho é assinado.  
  
 ASYMMETRIC KEY *Asym_key_name*  
 É o nome de uma chave assimétrica com que o procedimento armazenado, função, assembly ou gatilho é assinado.  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>Consulte Também  
 [sys.crypt_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [ADD SIGNATURE &#40;Transact-SQL&#41;](../../t-sql/statements/add-signature-transact-sql.md)  
  
  
