---
description: ENCRYPTBYASYMKEY (Transact-SQL)
title: ENCRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 42ffb61535beefeee149124adf7873cce78c1535
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111088"
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Essa função criptografa dados com uma chave assimétrica.  
  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*asym_key_ID*  
A ID de uma chave assimétrica no banco de dados. *asym_key_ID* tem um tipo de dados **int**.  
  
*cleartext*  
Um cadeia de caracteres de dados que `ENCRYPTBYASYMKEY` criptografará com a chave assimétrica. *texto não criptografado* pode ter um
 
+ **binary**
+ **char**
+ **nchar**
+ **nvarchar**
+ **varbinary**
  
ou
  
+ **varchar**
 
tipo de dados.  
  
**\@plaintext**  
Uma variável que contém um valor que `ENCRYPTBYASYMKEY` criptografará com a chave assimétrica. **\@plaintext** pode ter um
  
+ **binary**
+ **char**
+ **nchar**
+ **nvarchar**
+ **varbinary**
  
ou
  
+ **varchar**
 
tipo de dados.  
  
## <a name="return-types"></a>Tipos de retorno  
**varbinary**, com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentários  
Operações de criptografia e descriptografia que usam chaves assimétricas consomem recursos significativos e, portanto, tornam-se caras quando comparadas à descriptografia e criptografia de chave simétrica. Sugerimos que os desenvolvedores evitem operações de criptografia e de descriptografia de chave assimétrica ao trabalharem com grandes conjuntos de dados, por exemplo, conjuntos de dados do usuário armazenados em tabelas de banco de dados. Em vez disso, sugerimos que os desenvolvedores primeiro criptografem dados com uma chave simétrica forte e, em seguida, criptografem a chave simétrica com uma chave assimétrica.  
  
Dependendo do algoritmo, `ENCRYPTBYASYMKEY` retorna **NULL** se a entrada excede um certo número de bytes. Os limites específicos:

+ uma chave RSA de 512 bits pode criptografar até 53 bytes
+ uma chave RSA de 1024 bits pode criptografar até 117 bytes
+ uma chave RSA de 2048 bits pode criptografar até 245 bytes

No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tanto certificados quanto chaves assimétricas servem como wrappers sobre chaves RSA.  
  
## <a name="examples"></a>Exemplos  
Este exemplo criptografa o texto armazenado em `@cleartext` com a chave assimétrica `JanainaAsymKey02`. A instrução insere os dados criptografados na tabela `ProtectedData04`.  
  
```sql  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
