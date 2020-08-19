---
description: DECRYPTBYKEYAUTOCERT (Transact-SQL)
title: DECRYPTBYKEYAUTOCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 73aa01ab2817f9435791af4f2bb01ae81ef86fcc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417432"
---
# <a name="decryptbykeyautocert-transact-sql"></a>DECRYPTBYKEYAUTOCERT (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Essa função descriptografa dados com uma chave simétrica. Essa chave simétrica descriptografa automaticamente com um certificado.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *cert_ID*  
A ID do certificado usado para proteger a chave simétrica. *cert_ID* tem um tipo de dados **int**.  
  
*cert_password*  
A senha usada para criptografar a chave privada do certificado. Pode ter um valor `NULL` se a chave mestra do banco de dados proteger a chave privada. *cert_password* tem um tipo de dados **nvarchar**.  

'*ciphertext*'  
A cadeia de caracteres de dados criptografados com a chave. *ciphertext* tem um tipo de dados **varbinary**.  

@ciphertext  
Uma variável do tipo **varbinary** que contém dados criptografados com a chave.  

*add_authenticator*  
Indica se o processo de criptografia original incluía, e criptografava, um autenticador junto com o texto não criptografado. Deve corresponder ao valor passado para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) durante o processo de criptografia de dados. *add_authenticator* teria um valor de 1, se o processo de criptografia usasse um autenticador. *add_authenticator* tem um tipo de dados **int**.  
  
@add_authenticator  
Uma variável que indica se o processo de criptografia original incluía, e criptografava, um autenticador junto com o texto não criptografado. Deve corresponder ao valor passado para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) durante o processo de criptografia de dados. *\@add_authenticator* tem um tipo de dados **int**.  
  
*authenticator*  
Os dados usados como base para a geração do autenticador. Deve corresponder ao valor fornecido para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md). *authenticator* tem um tipo de dados **sysname**.  
  
@authenticator  
Uma variável que contém dados dos quais um autenticador é gerado. Deve corresponder ao valor fornecido para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md). *\@authenticator* tem um tipo de dados **sysname**.  
  
## <a name="return-types"></a>Tipos de retorno  
**varbinary**, com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentários  
`DECRYPTBYKEYAUTOCERT` combina a funcionalidade de `OPEN SYMMETRIC KEY` e de `DECRYPTBYKEY`. Em uma única operação, ele primeiro descriptografa uma chave simétrica e depois descriptografa o texto cifrado com ela.  
  
## <a name="permissions"></a>Permissões  
Requer a permissão `VIEW DEFINITION` na chave simétrica e a permissão `CONTROL` no certificado.   
  
## <a name="examples"></a>Exemplos  
Este exemplo mostra como `DECRYPTBYKEYAUTOCERT` pode simplificar o código de descriptografia. Esse código deve ser executado em um banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que ainda não tenha uma chave mestra de banco de dados.  
  
```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE CERTIFICATE HumanResources037   
   WITH SUBJECT = 'Sammamish HR',   
   EXPIRY_DATE = '10/31/2009';  
CREATE SYMMETRIC KEY SSN_Key_01 WITH ALGORITHM = DES  
    ENCRYPTION BY CERTIFICATE HumanResources037;  
GO  
----Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037 ;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
--  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key  
--2. Decrypt the data  
--3. Close the symmetric key  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
SELECT NationalIDNumber, EncryptedNationalIDNumber    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--OPTION TWO, using DecryptByKeyAutoCert()  
SELECT NationalIDNumber, EncryptedNationalIDNumber   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoCert ( cert_ID('HumanResources037') , NULL ,EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
