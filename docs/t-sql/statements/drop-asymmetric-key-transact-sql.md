---
title: "Remova a chave ASSIMÉTRICA (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP ASYMMETRIC KEY
- DROP_ASYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], removing
- removing asymmetric keys
- encryption [SQL Server], asymmetric keys
- DROP ASYMMETRIC KEY statement
- dropping asymmetric keys
- deleting asymmetric keys
- cryptography [SQL Server], asymmetric keys
ms.assetid: bf94ac07-9b62-4318-b55b-1eed8f3a1ac6
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f3737521ee178f9b7287f8d86e269973841d74c6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-asymmetric-key-transact-sql"></a>DROP ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove uma chave assimétrica do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP ASYMMETRIC KEY key_name [ REMOVE PROVIDER KEY ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *key_name*  
 É o nome da chave assimétrica a ser descartada do banco de dados.  
  
 REMOVE PROVIDER KEY  
 Remove uma chave EKM (Gerenciamento de Chave Extensível) de um dispositivo EKM. Para obter mais informações sobre o gerenciamento extensível de chaves, consulte [gerenciamento extensível de chaves &#40; EKM &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Comentários  
 Uma chave assimétrica com a qual uma chave simétrica no banco de dados foi criptografada, ou para a qual um usuário ou logon é mapeado, não pode ser descartada. Antes de descartar essa chave, você deve descartar qualquer usuário ou logon mapeados para ela. Você também deve descartar ou alterar qualquer chave simétrica criptografada com a chave assimétrica. Você pode usar a opção DROP ENCRYPTION de [ALTER SYMMETRIC KEY](../../t-sql/statements/alter-symmetric-key-transact-sql.md) para remover a criptografia por uma chave assimétrica.  
  
 Metadados de chaves assimétricas podem ser acessados usando o [asymmetric_keys](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md) exibição do catálogo. As chaves em si não podem ser exibidas diretamente de dentro do banco de dados.  
  
 Se a chave assimétrica for mapeada para uma chave EKM no dispositivo EKM e a opção REMOVE PROVIDER KEY não for especificada, a chave será descartada do banco de dados mas não do dispositivo, e um aviso será emitido. Um aviso será emitido.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL na chave assimétrica.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a chave assimétrica `MirandaXAsymKey6` do banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
DROP ASYMMETRIC KEY MirandaXAsymKey6;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER SYMMETRIC KEY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)  
  
  

