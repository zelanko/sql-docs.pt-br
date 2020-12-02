---
description: DECRYPTBYKEYAUTOASYMKEY (Transact-SQL)
title: DECRYPTBYKEYAUTOASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOASYMKEY_TSQL
- DECRYPTBYKEYAUTOASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOASYMSKEY function
ms.assetid: 5521d4cf-740c-4ede-98b6-4ba90b84e32d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4ac2905d7466b8a2aa3e8a823ab25f89d98ae96f
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128509"
---
# <a name="decryptbykeyautoasymkey-transact-sql"></a>DECRYPTBYKEYAUTOASYMKEY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Esta função descriptografa dados criptografados. Para fazer isso, ele primeiro descriptografa uma chave simétrica com uma chave assimétrica separada e, em seguida, descriptografa os dados criptografados com a chave simétrica extraída na primeira "etapa".  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DecryptByKeyAutoAsymKey ( akey_ID , akey_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *akey_ID*  
A ID da chave assimétrica usada para criptografar a chave simétrica. *akey_ID* tem um tipo de dados **int**.  
  
 *akey_password*  
A senha que protege a chave assimétrica. *akey_password* poderá ter um valor NULL se a chave mestra do banco de dados proteger a chave privada assimétrica. *akey_password* tem um tipo de dados **nvarchar**.  
  
 *ciphertext* Os dados criptografados com a chave. *ciphertext* tem um tipo de dados **varbinary**.  
  
 @ciphertext  
Uma variável do tipo **varbinary** que contém dados criptografados com a chave simétrica.  
  
 *add_authenticator*  
Indica se o processo de criptografia original incluía, e criptografava, um autenticador junto com o texto não criptografado. Deve corresponder ao valor passado para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) durante o processo de criptografia de dados. *add_authenticator* teria um valor de 1, se o processo de criptografia usasse um autenticador. *add_authenticator* tem um tipo de dados **int**.  
  
 @add_authenticator  
Uma variável que indica se o processo de criptografia original incluía, e criptografava, um autenticador junto com o texto não criptografado. Deve corresponder ao valor passado para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) durante o processo de criptografia de dados. *\@add_authenticator* tem um tipo de dados **int**.
  
 *authenticator*  
Os dados usados como base para a geração do autenticador. Deve corresponder ao valor fornecido para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md). *authenticator* tem um tipo de dados **sysname**.  
  
 @authenticator  
Uma variável que contém dados dos quais um autenticador é gerado. Deve corresponder ao valor fornecido para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md). *\@authenticator* tem um tipo de dados **sysname**.  
  
@add_authenticator  
Uma variável que indica se o processo de criptografia original incluía, e criptografava, um autenticador junto com o texto não criptografado. Deve corresponder ao valor passado para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) durante o processo de criptografia de dados. *\@add_authenticator* tem um tipo de dados **int**.  

*authenticator*  
Os dados usados como base para a geração do autenticador. Deve corresponder ao valor fornecido para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md). *authenticator* tem um tipo de dados **sysname**.

@authenticator  
Uma variável que contém dados dos quais um autenticador é gerado. Deve corresponder ao valor fornecido para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md). *\@authenticator* tem um tipo de dados **sysname**.  

## <a name="return-types"></a>Tipos de retorno  
**varbinary**, com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentários  
`DECRYPTBYKEYAUTOASYMKEY` combina a funcionalidade de `OPEN SYMMETRIC KEY` e de `DECRYPTBYKEY`. Em uma única operação, ele primeiro descriptografa uma chave simétrica e depois descriptografa o texto cifrado com ela.  
  
## <a name="permissions"></a>Permissões  
Requer a permissão `VIEW DEFINITION` na chave simétrica e a permissão `CONTROL` na chave assimétrica.  
  
## <a name="examples"></a>Exemplos
Este exemplo mostra como `DECRYPTBYKEYAUTOASYMKEY` pode simplificar o código de descriptografia. Esse código deve ser executado em um banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que ainda não tenha uma chave mestra de banco de dados.  

```sql  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE ASYMMETRIC KEY SSN_AKey   
    WITH ALGORITHM = RSA_2048 ;   
GO  
CREATE SYMMETRIC KEY SSN_Key_02 WITH ALGORITHM = DES  
    ENCRYPTION BY ASYMMETRIC KEY SSN_AKey;  
GO  
--  
--Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber2 varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber2  
    = EncryptByKey(Key_GUID('SSN_Key_02'), NationalIDNumber);  
GO  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key.  
--2. Decrypt the data.  
--3. Close the symmetric key.  
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
SELECT NationalIDNumber, EncryptedNationalIDNumber2    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--OPTION TWO, using DecryptByKeyAutoAsymKey()  
SELECT NationalIDNumber, EncryptedNationalIDNumber2   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoAsymKey ( AsymKey_ID('SSN_AKey') , NULL ,EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
