---
title: ENCRYPTBYKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYKEY_TSQL
- ENCRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- authenticators [SQL Server]
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYKEY function
- ENCRYPTBYKEY function
ms.assetid: 0e11f8c5-f79d-46c1-ab11-b68ef05d6787
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e0883513725000588fe53ee31939f331902ba147
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948877"
---
# <a name="encryptbykey-transact-sql"></a>ENCRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Criptografa dados usando uma chave simétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EncryptByKey ( key_GUID , { 'cleartext' | @cleartext }  
    [, { add_authenticator | @add_authenticator }  
     , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *key_GUID*  
 É o GUID da chave a ser usado para criptografar o *cleartext*. **uniqueidentifier**.  
  
 '*cleartext*'  
 São os dados que serão criptografados com a chave.  
  
 @cleartext  
 É uma variável do tipo **nvarchar**, **char**, **varchar**, **binary**, **varbinary** ou **nchar** que contém dados a serem criptografados com a chave.  
  
 *add_authenticator*  
 Indica se um autenticador será criptografado junto com o *cleartext*. Deve ser 1 ao usar um autenticador. **int**.  
  
 @add_authenticator  
 Indica se um autenticador será criptografado junto com o *cleartext*. Deve ser 1 ao usar um autenticador. **int**.  
  
 *authenticator*  
 São os dados dos quais será derivado um autenticador. **sysname**.  
  
 @authenticator  
 É uma variável que contém dados a partir dos quais o autenticador será derivado.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varbinary** com um tamanho máximo de 8.000 bytes.  
  
 Retorna o NULL se a chave não estiver aberta, se a chave não existir ou se a chave for uma chave de RC4 preterida e o banco de dados não estiver no nível de compatibilidade 110 ou superior.  
 
 Retorna NULL se o valor *cleartext* é NULL.
  
## <a name="remarks"></a>Remarks  
 EncryptByKey usa uma chave simétrica. Essa chave deve estar aberta. Se a chave simétrica já estiver aberta na sessão atual, não será necessário abri-la novamente no contexto da consulta.  
  
 O autenticador ajuda a impedir a substituição do valor inteiro de campos criptografados. Por exemplo, considere a tabela de dados de folha de pagamento a seguir.  
  
|Employee_ID|Standard_Title|Base_Pay|  
|------------------|---------------------|---------------|  
|345|Copy Room Assistant|Fskj%7^edhn00|  
|697|Chief Financial Officer|M0x8900f56543|  
|694|Data Entry Supervisor|Cvc97824%^34f|  
  
 Sem quebrar a criptografia, um usuário mal-intencionado pode deduzir informações significativas a partir do contexto em que o texto cifrado é armazenado. Como um Chief Financial Officer ganha mais do que um Copy Room Assistant, deduz-se que o valor criptografado como M0x8900f56543 seja maior do que o valor criptografado como Fskj%7^edhn00. Portanto, qualquer usuário com permissão ALTER na tabela pode conceder um aumento ao Copy Room Assistant substituindo os dados em seu campo Base_Pay por uma cópia dos dados armazenados no campo Base_Pay do Chief Financial Officer. Esse ataque de substituição do valor inteiro ignora completamente a criptografia.  
  
 Os ataques de substituição do valor inteiro podem ser impedidos adicionando-se informações contextuais ao texto não criptografado antes de criptografá-lo. Essas informações contextuais são usadas para verificar se os dados de texto não criptografado não foram movidos.  
  
 Se um parâmetro de autenticador for especificado no momento em que os dados são criptografados, o mesmo autenticador será necessário para descriptografar os dados usando o DecryptByKey. No momento da criptografia, um hash do autenticador é criptografado com o texto não criptografado. No momento da descriptografia, o mesmo autenticador deve ser passado para a DecryptByKey. Se não houver correspondência entre os dois, a descriptografia falhará. Isso indica que o valor foi movido desde que foi criptografado. Recomendamos usar uma coluna que contenha um valor exclusivo e inalterável como o autenticador. Se o valor do autenticador for alterado, você poderá perder o acesso aos dados.  
  
 A criptografia e a descriptografia simétricas são relativamente rápidas e adequadas para trabalhar com grandes quantidades de dados.  
  
> [!IMPORTANT]  
>  O uso das funções de criptografia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a configuração ANSI_PADDING OFF pode provocar perda de dados devido a conversões implícitas. Para obter mais informações sobre ANSI_PADDING, veja [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 A funcionalidade ilustrada nos seguintes exemplos baseia-se nas chaves e nos certificados criados em [Como: criptografar uma coluna de dados](../../relational-databases/security/encryption/encrypt-a-column-of-data.md).  
  
### <a name="a-encrypting-a-string-with-a-symmetric-key"></a>A. Criptografando uma cadeia de caracteres com uma chave simétrica  
 O exemplo a seguir adiciona uma coluna à tabela `Employee` e, em seguida, criptografa o valor do número de Social Security que é armazenado na coluna `NationalIDNumber`.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
  
-- Encrypt the value in column NationalIDNumber with symmetric key  
-- SSN_Key_01. Save the result in column EncryptedNationalIDNumber.  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
```  
  
### <a name="b-encrypting-a-record-together-with-an-authentication-value"></a>B. Criptografando um registro com um valor de autenticação  
  
```  
USE AdventureWorks2012;  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard   
    ADD CardNumber_Encrypted varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY CreditCards_Key11  
    DECRYPTION BY CERTIFICATE Sales09;  
  
-- Encrypt the value in column CardNumber with symmetric   
-- key CreditCards_Key11.  
-- Save the result in column CardNumber_Encrypted.    
UPDATE Sales.CreditCard  
SET CardNumber_Encrypted = EncryptByKey(Key_GUID('CreditCards_Key11'),   
    CardNumber, 1, CONVERT( varbinary, CreditCardID) );  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [HASHBYTES &#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
  
  
