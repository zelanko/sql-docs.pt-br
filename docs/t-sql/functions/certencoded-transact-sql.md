---
title: CERTENCODED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERTENCODED
- CERTENCODED_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTENCODED
ms.assetid: 677a0719-7b9a-4f0b-bc61-41634563f924
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6764a93f2dc1f6cb81d1c592a3392c12aa86bb41
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674984"
---
# <a name="certencoded-transact-sql"></a>CERTENCODED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Essa função retorna a parte pública de um certificado em formato binário. Essa função usa uma ID de certificado como argumento e retorna o certificado codificado. Para criar um novo certificado, passe o resultado binário para **CREATE CERTIFICATE… WITH BINARY**.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CERTENCODED ( cert_id )  
```  
  
## <a name="arguments"></a>Argumentos  
*cert_id*  
A **certificate_id** do certificado. Encontre esse valor em sys.certificates; a função [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md) o retornará também. *cert_id* tem um tipo de dados **int**.
  
## <a name="return-types"></a>Tipos de retorno
**varbinary**
  
## <a name="remarks"></a>Remarks  
Use **CERTENCODED** e **CERTPRIVATEKEY** em conjunto para retornar, em formato binário, diferentes partes de um certificado.
  
## <a name="permissions"></a>Permissões  
**CERTENCODED** está disponível publicamente.
  
## <a name="examples"></a>Exemplos  
  
### <a name="simple-example"></a>Exemplo simples  
Este exemplo cria um certificado chamado `Shipping04` e, em seguida, usa a função **CERTENCODED** para retornar a codificação binária do certificado. Este exemplo define a data de expiração do certificado como 31 de outubro de 2040.
  
```sql
CREATE DATABASE TEST1;
GO
USE TEST1
CREATE CERTIFICATE Shipping04
ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'
WITH SUBJECT = 'Sammamish Shipping Records',
EXPIRY_DATE = '20401031';
GO
SELECT CERTENCODED(CERT_ID('Shipping04'));
  
```  
  
### <a name="b-copying-a-certificate-to-another-database"></a>B. Copiando um certificado em outro banco de dados  
O exemplo mais complexo cria dois bancos de dados, `SOURCE_DB` e `TARGET_DB`. Em seguida, crie um certificado no `SOURCE_DB` e, depois, copie o certificado para o `TARGET_DB`. Por fim, demonstre que os dados criptografados no `SOURCE_DB` podem ser descriptografados no `TARGET_DB` usando a cópia do certificado.
  
Para criar o ambiente de exemplo, crie os bancos de dados `SOURCE_DB` e `TARGET_DB` e uma chave mestra em cada banco de dados. Em seguida, crie um certificado no `SOURCE_DB`.
  
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
  
Depois, extraia a descrição binária do certificado.
  
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
  
Em seguida, crie o certificado duplicado no banco de dados `TARGET_DB`. Modifique o código a seguir para que isto funcione, inserindo os dois valores binários – @CERTENC e @CERTPVK – retornados na etapa anterior. Não coloque esses valores entre aspas.
  
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
  
Esse código, executado como um único lote, demonstra que o `TARGET_DB` pode descriptografar os dados criptografados originalmente no `SOURCE_DB`.
  
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
  
## <a name="see-also"></a>Confira também
[Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
