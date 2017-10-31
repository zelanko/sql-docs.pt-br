---
title: CERTENCODED (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTENCODED
- CERTENCODED_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTENCODED
ms.assetid: 677a0719-7b9a-4f0b-bc61-41634563f924
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7596187fc97c0afd1df49f9de1e7ed168de5bcb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="certencoded-transact-sql"></a>CERTENCODED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna a parte pública de um certificado em formato binário. Essa função usa uma ID de certificado e retorna o certificado codificado. O resultado binário pode ser passado para **CREATE CERTIFICATE... COM binário** para criar um novo certificado.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CERTENCODED ( cert_id )  
```  
  
## <a name="arguments"></a>Argumentos  
*Cert_ID*  
É o **certificate_id** do certificado. Isso está disponível de Certificates ou usando o [CERT_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/cert-id-transact-sql.md) função. *Cert_ID* é do tipo **int**
  
## <a name="return-types"></a>Tipos de retorno
**varbinary**
  
## <a name="remarks"></a>Comentários  
**CERTENCODED** e **CERTPRIVATEKEY** são usados juntos para retornar diferentes partes de um certificado em formato binário.
  
## <a name="permissions"></a>Permissões  
**CERTENCODED** está disponível para o público.
  
## <a name="examples"></a>Exemplos  
  
### <a name="simple-example"></a>Exemplo simples  
O exemplo a seguir cria um certificado denominado `Shipping04` e, em seguida, usa o **CERTENCODED** função para retornar a codificação binária do certificado.
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE CERTIFICATE Shipping04   
ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20161031';  
GO  
SELECT CERTENCODED(CERT_ID('Shipping04'));  
  
```  
  
### <a name="b-copying-a-certificate-to-another-database"></a>B. Copiando um certificado em outro banco de dados  
O exemplo mais complicado a seguir, cria dois bancos de dados, `SOURCE_DB` e `TARGET_DB`. A meta é criar um certificado no `SOURCE_DB` e, em seguida, copiar o certificado no `TARGET_DB` e demonstrar que os dados criptografados no `SOURCE_DB` podem ser descriptografados no `TARGET_DB` usando a cópia do certificado.
  
Para criar o ambiente de exemplo, crie os bancos de dados `SOURCE_DB` e `TARGET_DB` e uma chave mestra em cada um. Em seguida, crie um certificado em `SOURCE_DB`.
  
```sql
USE master;  
GO  
CREATE DATABASE SOURCE_DB;  
GO  
USE SOURCE_DB;  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0URCE_DB KEY Pa$$W0rd';  
GO  
CREATE DATABASE TARGET_DB;  
GO  
USE TARGET_DB  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Pa$$W0rd in TARGET_DB';  
GO  
  
-- Create a certificate in SOURCE_DB  
USE SOURCE_DB;  
GO  
CREATE CERTIFICATE SOURCE_CERT WITH SUBJECT = 'SOURCE_CERTIFICATE';  
GO  
```  
  
Agora extraia a descrição binária do certificado.
  
```sql
DECLARE @CERTENC VARBINARY(MAX);  
DECLARE @CERTPVK VARBINARY(MAX);  
SELECT @CERTENC = CERTENCODED(CERT_ID('SOURCE_CERT'));  
SELECT @CERTPVK = CERTPRIVATEKEY(CERT_ID('SOURCE_CERT'),  
       'CertEncryptionPa$$word');  
SELECT @CERTENC AS BinaryCertificate;  
SELECT @CERTPVK AS EncryptedBinaryCertificate;  
GO  
```  
  
Crie o certificado duplicado no banco de dados `TARGET_DB`. Você deve modificar o código a seguir, inserindo os dois valores binários retornados na etapa anterior.
  
```sql
-- Create the duplicate certificate in the TARGET_DB database  
USE TARGET_DB  
GO  
CREATE CERTIFICATE TARGET_CERT  
FROM BINARY = <insert the binary value of the @CERTENC variable>  
WITH PRIVATE KEY (  
BINARY = <insert the binary value of the @CERTPVK variable>  
, DECRYPTION BY PASSWORD = 'CertEncryptionPa$$word');  
-- Compare the certificates in the two databases  
-- The two certificates should be the same   
-- except for name and (possibly) the certificate_id  
SELECT * FROM SOURCE_DB.sys.certificates  
UNION  
SELECT * FROM TARGET_DB.sys.certificates;  
```  
  
O código a seguir, executado como um único lote, demonstra que os dados criptografados no `SOURCE_DB` podem ser descriptografados no `TARGET_DB`.
  
```sql
USE SOURCE_DB;  
  
DECLARE @CLEARTEXT nvarchar(100);  
DECLARE @CIPHERTEXT varbinary(8000);  
DECLARE @UNCIPHEREDTEXT_Source nvarchar(100);  
SET @CLEARTEXT = N'Hello World';  
SET @CIPHERTEXT = ENCRYPTBYCERT(CERT_ID('SOURCE_CERT'), @CLEARTEXT);  
SET @UNCIPHEREDTEXT_Source =   
    DECRYPTBYCERT(CERT_ID('SOURCE_CERT'), @CIPHERTEXT)  
-- Encryption and decryption result in SOURCE_DB  
SELECT @CLEARTEXT AS SourceClearText, @CIPHERTEXT AS SourceCipherText,   
       @UNCIPHEREDTEXT_Source AS SourceDecryptedText;  
  
-- SWITCH DATABASE  
USE TARGET_DB;  
  
DECLARE @UNCIPHEREDTEXT_Target nvarchar(100);  
SET @UNCIPHEREDTEXT_Target = DECRYPTBYCERT(CERT_ID('TARGET_CERT'), @CIPHERTEXT);  
-- Encryption and decryption result in TARGET_DB  
SELECT @CLEARTEXT AS ClearTextInTarget, @CIPHERTEXT AS CipherTextInTarget, @UNCIPHEREDTEXT_Target AS DecriptedTextInTarget;   
GO  
```  
  
## <a name="see-also"></a>Consulte também
[Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[CERTPRIVATEKEY &#40; Transact-SQL &#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  

