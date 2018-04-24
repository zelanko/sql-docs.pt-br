---
title: DECRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1744860b550142f274e23ca81da7792fa478df0b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Descriptografa dados com uma chave assimétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Asym_Key_ID*  
 É a ID de uma chave assimétrica no banco de dados. *Asym_Key_ID* é **int**.  
  
 *ciphertext*  
 É uma cadeia de caracteres de dados que foi criptografada com a chave assimétrica.  
  
 @ciphertext  
 É uma variável do tipo **varbinary** que contém dados que foram criptografados com a chave assimétrica.  
  
 *Asym_Key_Password*  
 É a senha que foi usada para criptografar a chave assimétrica no banco de dados.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varbinary** com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Remarks  
 A criptografia/descriptografia com uma chave assimétrica é muito dispendiosa em comparação a criptografia/descriptografia com uma chave simétrica. Não recomendamos o uso de uma chave assimétrica ao trabalhar com grandes conjuntos de dados, como os dados de usuário em tabelas.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL na chave assimétrica.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descriptografa o texto cifrado que foi criptografado com a chave assimétrica `JanainaAsymKey02`, que foi armazenada em `AdventureWorks2012.ProtectedData04`. Os dados retornados são descriptografados com a chave assimétrica `JanainaAsymKey02`, que foi descriptografada com a senha `pGFD4bb925DGvbd2439587y`. O texto sem formatação é convertido no tipo **nvarchar**.  
  
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
  
  
