---
description: ENCRYPTBYPASSPHRASE (Transact-SQL)
title: ENCRYPTBYPASSPHRASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYPASSPHRASE
- ENCRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYPASSPHRASE function
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYPASSPHRASE function
ms.assetid: f8dbb9e6-94d6-40d7-8b38-6833a409d597
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f8e11d7e9f36d6619c626d9387cce766fbce5b0d
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116782"
---
# <a name="encryptbypassphrase-transact-sql"></a>ENCRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Criptografe os dados com uma senha com o uso do algoritmo TRIPLE DES com um comprimento de chave de 128 bits.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
EncryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'cleartext' | @cleartext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *passphrase*  
 Uma frase secreta a partir da qual gerar uma chave simétrica.  
  
 @passphrase  
 Uma variável do tipo **nvarchar**, **char**, **varchar**, **binary**, **varbinary** ou **nchar** contendo uma frase secreta da qual gerar uma chave simétrica.  
  
 *cleartext*  
 O texto não criptografado a ser criptografado.  
  
 @cleartext  
 Uma variável do tipo **nvarchar**, **char**, **varchar**, **binary**, **varbinary** ou **nchar** contendo o texto não criptografado. O tamanho máximo é 8.000 bytes.  
  
 *add_authenticator*  
 Indica se um autenticador será criptografado junto com o texto não criptografado. 1 se um autenticador for adicionado. **int**.  
  
 @add_authenticator  
 Indica se um hash será criptografado junto com o texto não criptografado.  
  
 *authenticator*  
 Dados do qual derivar um autenticador. **sysname**.  
  
 @authenticator  
 Uma variável contendo dados a partir dos quais o autenticador será derivado.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varbinary** com no máximo 8.000 bytes.  
  
## <a name="remarks"></a>Comentários  
 Uma frase secreta é uma senha que inclui espaços. A vantagem de usar uma frase secreta é o fato de ser mais fácil lembrar uma frase ou sentença significativa do que uma cadeia de caracteres comparavelmente longa.  
  
 Esta função não verifica a complexidade da senha.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir atualiza um registro na tabela `SalesCreditCard` e criptografa o valor do número de cartão de crédito armazenado na coluna `CardNumber_EncryptedbyPassphrase`, usando a chave primária como um autenticador.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard   
    ADD CardNumber_EncryptedbyPassphrase VARBINARY(256);   
GO  
-- First get the passphrase from the user.  
DECLARE @PassphraseEnteredByUser NVARCHAR(128);  
SET @PassphraseEnteredByUser   
    = 'A little learning is a dangerous thing!';  
  
-- Update the record for the user's credit card.  
-- In this case, the record is number 3681.  
UPDATE Sales.CreditCard  
SET CardNumber_EncryptedbyPassphrase = EncryptByPassPhrase(@PassphraseEnteredByUser  
    , CardNumber, 1, CONVERT(varbinary, CreditCardID))  
WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DECRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbypassphrase-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
