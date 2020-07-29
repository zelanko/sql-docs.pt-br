---
title: ENCRYPTBYCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYCERT
- ENCRYPTBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], encryption
- encryption [SQL Server], certificates
- ENCRYPTBYCERT function
ms.assetid: ab66441f-e2d2-4e3a-bcae-bcc09e12f3c1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 801d2af4bc83b974761c1bd11982e0943460cf92
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112991"
---
# <a name="encryptbycert-transact-sql"></a>ENCRYPTBYCERT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Criptografa dados com a chave pública de um certificado.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
EncryptByCert ( certificate_ID , { 'cleartext' | @cleartext } )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
_certificate\_ID_  
A ID de um certificado no banco de dados. **int**.  
  
_cleartext_  
Uma cadeia de caracteres de dados que serão criptografados com o certificado.  
  
**\@cleartext**  
Uma variável de um dos seguintes tipos, que contém dados a serem criptografados com a chave pública do certificado:

* **nvarchar** 
* **char**
* **varchar**
* **binary** 
* **varbinary**
* **nchar**
  
## <a name="return-types"></a>Tipos de retorno  
**varbinary** com um tamanho máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentários  
Essa função criptografa dados com a chave pública do certificado. O texto cifrado só pode ser decifrado com a chave privada correspondente. Essas transformações assimétricas são muito caras comparadas à criptografia e descriptografia com o uso de uma chave simétrica. Assim, a criptografia assimétrica não é recomendada ao trabalhar com grandes conjuntos de dados.
  
## <a name="examples"></a>Exemplos  
Este exemplo criptografa o texto não criptografado armazenado em `@cleartext` com o certificado chamado `JanainaCert02`. Os dados criptografados são inseridos na tabela `ProtectedData04`.  
  
```  
INSERT INTO [AdventureWorks2012].[ProtectedData04]   
    VALUES ( N'Data encrypted by certificate ''Shipping04''',  
    EncryptByCert(Cert_ID('JanainaCert02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[DECRYPTBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbycert-transact-sql.md)   
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
[ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
[DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
[BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
[Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
