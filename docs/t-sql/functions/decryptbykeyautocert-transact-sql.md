---
title: DECRYPTBYKEYAUTOCERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/09/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0842000cd08e3ca82dab181f32ae96f4a0280d5d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# DECRYPTBYKEYAUTOCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descriptografa usando uma chave simétrica que é decifrada automaticamente com um certificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Sintaxe  
  
```  
  
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## Argumentos  
 *cert_ID*  
 É a ID de certificado usada para proteger a chave simétrica. *cert_ID* é **int**.  
  
 *cert_password*  
 É a senha que protege a chave privada do certificado. Poderá ser NULL se a chave privada estiver protegida pela chave mestra do banco de dados. *cert_password* é **nvarchar**.  
  
 '*texto cifrado*'  
 São os dados criptografados com a chave. *texto cifrado* é **varbinary**.  
  
 @ciphertext  
 É uma variável do tipo **varbinary** que contém dados que foram criptografados com a chave.  
  
 *add_authenticator*  
 Indica se um autenticador foi criptografado junto com o texto não criptografado. Deve ser o mesmo valor que é passado para EncryptByKey ao criptografar os dados. É **1** se um autenticador foi usado. *add_authenticator* é **int**.  
  
 @add_authenticator  
 Indica se um autenticador foi criptografado junto com o texto não criptografado. Deve ser igual ao valor que é passado para EncryptByKey ao criptografar os dados.  
  
 *autenticador*  
 São os dados a partir dos quais um autenticador é gerado. Deve corresponder ao valor fornecido para EncryptByKey. *autenticador* é **sysname**.  
  
 @authenticator  
 É uma variável que contém dados a partir dos quais um autenticador é gerado. Deve corresponder ao valor fornecido para EncryptByKey.  
  
## Tipos de retorno  
 **varbinary** com um tamanho máximo de 8.000 bytes.  
  
## Comentários  
 DecryptByKeyAutoCert combina a funcionalidade OPEN SYMMETRIC KEY e DecryptByKey. Em uma única operação, ele descriptografa uma chave simétrica e a usa para descriptografar texto codificado.  
  
## Permissões  
 Requer a permissão VIEW DEFINITION na chave simétrica e a permissão CONTROL no certificado.  
  
## Exemplos  
 O exemplo a seguir mostra como `DecryptByKeyAutoCert` pode ser usado para simplificar código que executa uma descriptografia. Esse código deve ser executado em um banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que ainda não tenha uma chave mestra de banco de dados.  
  
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
  
## Consulte também  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

