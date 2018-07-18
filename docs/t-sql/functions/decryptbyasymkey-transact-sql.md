---
title: DECRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
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
- DECRYPTBYASYMKEY
- DECRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], DECRYPTBYASYMKEY function
- DECRYPTBYASYMKEY function
- decryption [SQL Server], asymmetric keys
ms.assetid: d9ebcd30-f01c-4cfe-b95e-ffe6ea13788b
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1e002b65eb3136947e3785d6068b695001338447
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37791037"
---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essa função usa uma chave simétrica para descriptografar dados criptografados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Asym_Key_ID*  
A ID de uma chave assimétrica no banco de dados. *Asym_Key_ID* tem um tipo de dados **int**.  
  
 *ciphertext*  
A cadeia de caracteres de dados criptografados com a chave assimétrica.  
  
 @ciphertext  
Uma variável do tipo **varbinary** que contém dados criptografados com a chave assimétrica.  
  
 *Asym_Key_Password*  
A senha usada para criptografar a chave assimétrica no banco de dados.  
  
## <a name="return-types"></a>Tipos de retorno  
**varbinary**, com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Remarks  
Compara com a criptografia/descriptografia simétrica, a criptografia/descriptografia de chave assimétrica tem um alto custo. Ao trabalhar com grandes conjuntos de dados, por exemplo, dados de usuário armazenados em tabelas, sugerimos que os desenvolvedores evitem a criptografia/descriptografia de chave assimétrica.  
  
## <a name="permissions"></a>Permissões  
`DECRYPTBYASYMKEY` requer a permissão CONTROL na chave assimétrica.  
  
## <a name="examples"></a>Exemplos  
Este exemplo descriptografa o texto cifrado originalmente criptografado com a chave assimétrica `JanainaAsymKey02`. `AdventureWorks2012.ProtectedData04` armazenava essa chave assimétrica. O exemplo descriptografou os dados retornados com a chave assimétrica `JanainaAsymKey02`. O exemplo usou a senha `pGFD4bb925DGvbd2439587y` para descriptografar a chave assimétrica. O exemplo converteu o texto não criptografado retornado no tipo **nvarchar**.  
  
```  
SELECT CONVERT(nvarchar(max),  
    DecryptByAsymKey( AsymKey_Id('JanainaAsymKey02'),   
    ProtectedData, N'pGFD4bb925DGvbd2439587y' ))   
AS DecryptedData   
FROM [AdventureWorks2012].[Sales].[ProtectedData04]   
WHERE Description = N'encrypted by asym key''JanainaAsymKey02''';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
