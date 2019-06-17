---
title: DECRYPTBYCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3021bfc31b6fe8e5681ca220434f8644b6a4afe9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65945527"
---
# <a name="decryptbycert-transact-sql"></a>DECRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essa função usa a chave privada de um certificado para descriptografar dados criptografados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DecryptByCert ( certificate_ID , { 'ciphertext' | @ciphertext }   
    [ , { 'cert_password' | @cert_password } ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *certificate_ID*  
A ID de um certificado no banco de dados. *certificate_ID* tem um tipo de dados **int**.  
  
 *ciphertext*  
A cadeia de caracteres de dados criptografados com a chave pública do certificado.  
  
 @ciphertext  
Uma variável do tipo **varbinary** que contém dados criptografados com o certificado.  
  
 *cert_password*  
A senha usada para criptografar a chave privada do certificado. *cert_password* deve ter um formato de dados Unicode.  
  
 @cert_password  
Uma variável do tipo **nchar** ou **nvarchar** que contém a senha usada para criptografar a chave privada do certificado. *@cert_password* deve ter um formato de dados Unicode.  

## <a name="return-types"></a>Tipos de retorno  
**varbinary**, com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Remarks  
Essa função descriptografa dados com a chave privada de um certificado. As transformações criptográficas que usam chaves assimétricas consomem recursos significativos. Portanto, sugerimos que os desenvolvedores evitem o uso de [ENCRYPTBYCERT](./encryptbycert-transact-sql.md) e de DECRYPTBYCERT para criptografia/descriptografia de dados do usuário de rotina.  

## <a name="permissions"></a>Permissões  
`DECRYPTBYCERT` requer a permissão CONTROL no certificado.  
  
## <a name="examples"></a>Exemplos  
Este exemplo seleciona linhas de `[AdventureWorks2012].[ProtectedData04]` marcadas como dados originalmente criptografados pelo certificado `JanainaCert02`. Primeiro o exemplo descriptografa a chave privada do certificado `JanainaCert02` com a senha do certificado `pGFD4bb925DGvbd2439587y`. Em seguida, o exemplo descriptografa o texto cifrado com essa chave privada. O exemplo converte os dados descriptografados de **varbinary** em **nvarchar**.  

```  
SELECT convert(nvarchar(max), DecryptByCert(Cert_Id('JanainaCert02'),  
    ProtectedData, N'pGFD4bb925DGvbd2439587y'))  
FROM [AdventureWorks2012].[ProtectedData04]   
WHERE Description   
    = N'data encrypted by certificate '' JanainaCert02''';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ENCRYPTBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
