---
title: DECRYPTBYPASSPHRASE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYPASSPHRASE
- DECRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], DECRYPTBYPASSPHRASE function
- DECRYPTBYPASSPHRASE function
ms.assetid: ca34b5cd-07b3-4dca-b66a-ed8c6a826c95
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dc2880109f8b58cc1712b58f68883cab1cace348
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="decryptbypassphrase-transact-sql"></a>DECRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Descriptografa dados que foram criptografados com uma frase secreta.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DecryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *passphrase*  
 É a senha que será usada para gerar a chave para descriptografia.  
  
 @passphrase  
 É uma variável do tipo **nvarchar**, **char**, **varchar** ou **nchar** que contém a frase secreta que será usada para gerar a chave para descriptografia.  
  
 '*ciphertext*'  
 É o texto cifrado a ser descriptografado.  
  
 @ciphertext  
 É uma variável do tipo **varbinary** que contém o texto cifrado. O tamanho máximo é 8.000 bytes.  
  
 *add_authenticator*  
 Indica se um autenticador foi criptografado junto com o texto não criptografado. É 1 se um autenticador tiver sido usado. **int**.  
  
 @add_authenticator  
 Indica se um autenticador foi criptografado junto com o texto não criptografado. É 1 se um autenticador tiver sido usado. **int**.  
  
 *authenticator*  
 São os dados do autenticador. **sysname**.  
  
 @authenticator  
 É uma variável que contém dados a partir dos quais o autenticador será derivado.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varbinary** com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Remarks  
 Nenhuma permissão é necessária para executar esta função.  
  
 Retorna NULL se a frase secreta errada ou informações do autenticador forem usadas.  
  
 A frase secreta é usada para gerar uma chave de descriptografia, que não será persistida.  
  
 Se um autenticador tiver sido incluído que quando o texto cifrado foi criptografado, o autenticador deve ser fornecido no momento da descriptografia. Se o valor do autenticador fornecido no momento da descriptografia não coincidir com o valor criptografado com os dados, a descriptografia falhará.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descriptografa o registro atualizado em [EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
-- Get the pass phrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
= 'A little learning is a dangerous thing!';  
  
-- Decrypt the encrypted record.  
SELECT CardNumber, CardNumber_EncryptedbyPassphrase   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByPassphrase(@PassphraseEnteredByUser, CardNumber_EncryptedbyPassphrase, 1   
    , CONVERT(varbinary, CreditCardID)))  
    AS 'Decrypted card number' FROM Sales.CreditCard   
    WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
  
  
