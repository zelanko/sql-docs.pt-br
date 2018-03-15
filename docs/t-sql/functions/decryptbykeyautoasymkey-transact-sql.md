---
title: DECRYPTBYKEYAUTOASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/09/2015
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOASYMKEY_TSQL
- DECRYPTBYKEYAUTOASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOASYMSKEY function
ms.assetid: 5521d4cf-740c-4ede-98b6-4ba90b84e32d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d2e418ce7df83c5c10e6af9517b087ccc877273
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="decryptbykeyautoasymkey-transact-sql"></a>DECRYPTBYKEYAUTOASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descriptografa usando uma chave simétrica que é automaticamente descriptografada com uma chave assimétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DecryptByKeyAutoAsymKey ( akey_ID , akey_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *akey_ID*  
 É a ID da chave assimétrica usada para proteger a chave simétrica. *akey_ID* é **int**.  
  
 *akey_password*  
 É a senha que protege a chave privada da chave assimétrica. Poderá ser NULL se a chave privada estiver protegida pela chave mestra do banco de dados. *akey_password* é **nvarchar**.  
  
 '*ciphertext*'  
 São os dados criptografados com a chave. O *ciphertext* é **varbinary**.  
  
 @ciphertext  
 É uma variável do tipo **varbinary** que contém dados que foram criptografados com a chave.  
  
 *add_authenticator*  
 Indica se um autenticador foi criptografado junto com o texto não criptografado. Deve ser igual ao valor que é passado para EncryptByKey ao criptografar os dados. É 1 se um autenticador tiver sido usado. *add_authenticator* é **int**.  
  
 @add_authenticator  
 Indica se um autenticador foi criptografado junto com o texto não criptografado. Deve ser igual ao valor que é passado para EncryptByKey ao criptografar os dados.  
  
 *authenticator*  
 São os dados a partir dos quais um autenticador é gerado. Deve corresponder ao valor fornecido para EncryptByKey. O *authenticator* é **sysname**.  
  
 @authenticator  
 É uma variável que contém dados a partir dos quais um autenticador é gerado. Deve corresponder ao valor fornecido para EncryptByKey.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varbinary** com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Remarks  
 DecryptByKeyAutoAsymKey combina a funcionalidade de OPEN SYMMETRIC KEY e DecryptByKey. Em uma única operação, ele descriptografa uma chave simétrica e a utiliza para descriptografar texto cifrado.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DEFINITION na chave simétrica e a permissão CONTROL na chave assimétrica.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como `DecryptByKeyAutoAsymKey` pode ser usado para simplificar código que executa uma descriptografia. Esse código deve ser executado em um banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que ainda não tenha uma chave mestra de banco de dados.  
  
```  
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
  
  
