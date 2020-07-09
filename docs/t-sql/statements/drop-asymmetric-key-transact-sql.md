---
title: DROP ASYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 338e86328ed41ef0e2da4d4e9a6c20c5f0551f53
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85766552"
---
# <a name="drop-asymmetric-key-transact-sql"></a>DROP ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Remove uma chave assimétrica do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP ASYMMETRIC KEY key_name [ REMOVE PROVIDER KEY ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *key_name*  
 É o nome da chave assimétrica a ser descartada do banco de dados.  
  
 REMOVE PROVIDER KEY  
 Remove uma chave EKM (Gerenciamento Extensível de Chaves) de um dispositivo EKM. Para obter mais informações sobre o gerenciamento extensível de chaves, consulte [EKM &#40;Gerenciamento extensível de chaves&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Comentários  
 Uma chave assimétrica com a qual uma chave simétrica no banco de dados foi criptografada, ou para a qual um usuário ou logon é mapeado, não pode ser descartada. Antes de descartar essa chave, você deve descartar qualquer usuário ou logon mapeados para ela. Você também deve descartar ou alterar qualquer chave simétrica criptografada com a chave assimétrica. É possível usar a opção DROP ENCRYPTION de [ALTER SYMMETRIC KEY](../../t-sql/statements/alter-symmetric-key-transact-sql.md) para remover a criptografia por meio de uma chave assimétrica.  
  
 Os metadados de chaves assimétricas podem ser acessados com a exibição do catálogo [sys.asymmetric_keys](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md). As chaves em si não podem ser exibidas diretamente de dentro do banco de dados.  
  
 Se a chave assimétrica for mapeada para uma chave EKM no dispositivo EKM e a opção REMOVE PROVIDER KEY não for especificada, a chave será descartada do banco de dados mas não do dispositivo, e um aviso será emitido. Um aviso será emitido.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL na chave assimétrica.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a chave assimétrica `MirandaXAsymKey6` do banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
DROP ASYMMETRIC KEY MirandaXAsymKey6;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)  
  
  
