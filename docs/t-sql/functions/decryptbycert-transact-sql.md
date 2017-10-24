---
title: DECRYPTBYCERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DecryptByCert_TSQL
- DECRYPTBYCERT
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], decryption
- decryption [SQL Server], certificates
- DECRYPTBYCERT function
ms.assetid: 4950d787-40fa-4e26-bce8-2cb2ceca12fb
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ebdc328e49635af823cd64e8539ee5b7cfa95c76
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbycert-transact-sql"></a>DECRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Descriptografa dados com a chave privada de um certificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DecryptByCert ( certificate_ID , { 'ciphertext' | @ciphertext }   
    [ , { 'cert_password' | @cert_password } ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *certificate_ID*  
 É a ID de um certificado no banco de dados. *certificado*ID é **int**.  
  
 *texto cifrado*  
 É uma cadeia de dados que foi criptografada com a chave pública do certificado.  
  
 @ciphertext  
 É uma variável do tipo **varbinary** que contém dados que foram criptografados com o certificado.  
  
 *cert_password*  
 É a senha que foi usada para criptografar a chave privada do certificado. Deve ser Unicode.  
  
 @cert_password  
 É uma variável do tipo **nchar** ou **nvarchar** que contém a senha que foi usada para criptografar a chave privada do certificado. Deve ser Unicode.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varbinary** com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentários  
 Essa função descriptografa dados com a chave privada de um certificado. As transformações criptográficas que usam chaves assimétricas consomem recursos significativos. Portanto, EncryptByCert e DecryptByCert não são adequados para a criptografia de rotina de dados de usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no certificado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir seleciona linhas de `[AdventureWorks2012].[ProtectedData04]` marcadas como `data encrypted by certificate JanainaCert02`. O exemplo descriptografa o texto cifrado com a chave privada do certificado `JanainaCert02`, que ele primeiro descriptografa com a senha do certificado, `pGFD4bb925DGvbd2439587y`. Os dados descriptografados são convertidos de **varbinary** para **nvarchar**.  
  
```  
SELECT convert(nvarchar(max), DecryptByCert(Cert_Id('JanainaCert02'),  
    ProtectedData, N'pGFD4bb925DGvbd2439587y'))  
FROM [AdventureWorks2012].[ProtectedData04]   
WHERE Description   
    = N'data encrypted by certificate '' JanainaCert02''';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [ENCRYPTBYCERT & #40; Transact-SQL & #41;](../../t-sql/functions/encryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE & #40; Transact-SQL & #41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [Remover certificado & #40; Transact-SQL & #41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

