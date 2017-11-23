---
title: ENCRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
caps.latest.revision: "35"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6ef212d976ca8f84881695d85e56f5ab1cbca020
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Criptografa dados com uma chave assimétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Asym_Key_ID*  
 É a ID de uma chave assimétrica no banco de dados. **int**.  
  
 *texto não criptografado*  
 É uma cadeia de caracteres de dados que será criptografada com a chave assimétrica.  
  
 **@plaintext**  
 É uma variável do tipo **nvarchar**, **char**, **varchar**, **binário**, **varbinary**, ou **nchar** que contém dados a serem criptografados com a chave assimétrica.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varbinary** com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentários  
 A criptografia e descriptografia com uma chave assimétrica é muito dispendiosa comparada à criptografia e descriptografia com uma chave simétrica. Recomendamos que você não criptografe conjuntos de dados grandes, como dados de usuário em tabelas, usando uma chave assimétrica. Em vez disso, criptografe os dados usando uma chave simétrica forte e criptografe a chave simétrica usando uma chave assimétrica.  
  
 **EncryptByAsymKey** retornar **nulo** se a entrada exceder um determinado número de bytes, dependendo do algoritmo. Os limites são: uma chave RSA de 512 bits pode criptografar até 53 bytes, uma chave de 1024 bits pode criptografar até 117 bytes e uma chave de 2048 bits pode criptografar até 245 bytes. (Observe que no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], certificados e chaves assimétricas são wrappers sobre chaves RSA.)  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir criptografa o texto armazenado em `@cleartext` com a chave assimétrica `JanainaAsymKey02`. Os dados criptografados são inseridos no `ProtectedData04` tabela.  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [DECRYPTBYASYMKEY &#40; Transact-SQL &#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
