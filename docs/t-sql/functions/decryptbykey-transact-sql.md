---
title: DECRYPTBYKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DecryptByKey_TSQL
- DECRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], DecryptByKey function
- decryption [SQL Server], keys
- decryption [SQL Server], symmetric keys
- DECRYPTBYKEY function
ms.assetid: 6edf121f-ac62-4dae-90e6-6938f32603c9
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 61e984a45f2f5a7b2d675ec574fda255c4747642
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37783057"
---
# <a name="decryptbykey-transact-sql"></a>DECRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essa função usa uma chave simétrica para descriptografar dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DecryptByKey ( { 'ciphertext' | @ciphertext }   
    [ , add_authenticator, { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*ciphertext*  
Uma variável do tipo **varbinary** que contém dados criptografados com a chave.  
  
**@ciphertext**  
Uma variável do tipo **varbinary** que contém dados criptografados com a chave.  
  
 *add_authenticator*  
Indica se o processo de criptografia original incluía, e criptografava, um autenticador junto com o texto não criptografado. Deve corresponder ao valor passado para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) durante o processo de criptografia de dados. *add_authenticator* tem um tipo de dados **int**.  
  
 *authenticator*  
Os dados usados como base para a geração do autenticador. Deve corresponder ao valor fornecido para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md). *authenticator* tem um tipo de dados **sysname**.  

**@authenticator**  
Uma variável que contém dados dos quais um autenticador é gerado. Deve corresponder ao valor fornecido para [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md). *@authenticator* tem um tipo de dados **sysname**.  

## <a name="return-types"></a>Tipos de retorno  
**varbinary**, com um tamanho máximo de 8.000 bytes. `DECRYPTBYKEY` retornará NULL se a chave simétrica usada para criptografia de dados não estiver aberta ou se *ciphertext* for NULL.  
  
## <a name="remarks"></a>Remarks  
`DECRYPTBYKEY` usa uma chave simétrica. O banco de dados deve ter essa chave simétrica já aberta. `DECRYPTBYKEY` permitirá várias chaves abertas ao mesmo tempo. Não é necessário abrir a chave imediatamente antes da descriptografia do texto cifrado.  
  
Normalmente a criptografia e descriptografia simétricas operam de maneira relativamente rápida e funciona bem para operações que envolvem grandes volumes de dados.  
  
## <a name="permissions"></a>Permissões  
A chave simétrica já deve estar aberta na sessão atual. Consulte [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md) para obter mais informações.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-decrypting-by-using-a-symmetric-key"></a>A. Descriptografando com o uso de uma chave simétrica  
Este exemplo descriptografa o texto cifrado com uma chave simétrica.  
  
```  
-- First, open the symmetric key with which to decrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
GO  
  
-- Now list the original ID, the encrypted ID, and the   
-- decrypted ciphertext. If the decryption worked, the original  
-- and the decrypted ID will match.  
SELECT NationalIDNumber, EncryptedNationalID   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalID))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-decrypting-by-using-a-symmetric-key-and-an-authenticating-hash"></a>B. Descriptografando com o uso de uma chave simétrica e um hash de autenticação  
Este exemplo descriptografa dados originalmente criptografados juntamente com um autenticador.  
  
```  
-- First, open the symmetric key with which to decrypt the data  
OPEN SYMMETRIC KEY CreditCards_Key11  
   DECRYPTION BY CERTIFICATE Sales09;  
GO  
  
-- Now list the original card number, the encrypted card number,  
-- and the decrypted ciphertext. If the decryption worked,   
-- the original number will match the decrypted number.  
SELECT CardNumber, CardNumber_Encrypted   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByKey(CardNumber_Encrypted, 1 ,   
    HashBytes('SHA1', CONVERT(varbinary, CreditCardID))))   
    AS 'Decrypted card number' FROM Sales.CreditCard;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
