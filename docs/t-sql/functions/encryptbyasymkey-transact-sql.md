---
title: ENCRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 212ce15f0d28b16b81a9c07d785c129b039cdc6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Criptografa dados com uma chave assimétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Asym_Key_ID*  
 É a ID de uma chave assimétrica no banco de dados. **int**.  
  
 *cleartext*  
 É uma cadeia de caracteres de dados que será criptografada com a chave assimétrica.  
  
 **@plaintext**  
 É uma variável do tipo **nvarchar**, **char**, **varchar**, **binary**, **varbinary** ou **nchar** que contém dados a serem criptografados com a chave assimétrica.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varbinary** com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Remarks  
 A criptografia e descriptografia com uma chave assimétrica é muito dispendiosa comparada à criptografia e descriptografia com uma chave simétrica. Recomendamos que você não criptografe conjuntos de dados grandes, como dados de usuário em tabelas, usando uma chave assimétrica. Em vez disso, criptografe os dados usando uma chave simétrica forte e criptografe a chave simétrica usando uma chave assimétrica.  
  
 **EncryptByAsymKey** retorna **NULL** se a entrada excede determinado número de bytes, dependendo do algoritmo. Os limites são: uma chave RSA de 512 bits pode criptografar até 53 bytes, uma chave de 1.024 bits pode criptografar até 117 bytes e uma chave de 2.048 bits pode criptografar até 245 bytes. (Observe que no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], certificados e chaves assimétricas são wrappers sobre chaves RSA.)  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir criptografa o texto armazenado em `@cleartext` com a chave assimétrica `JanainaAsymKey02`. Os dados criptografados são inseridos na tabela `ProtectedData04`.  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
