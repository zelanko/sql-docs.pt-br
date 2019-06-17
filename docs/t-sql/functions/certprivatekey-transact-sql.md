---
title: CERTPRIVATEKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERTPRIVATEKEY
- CERTPRIVATEKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTPRIVATEKEY
ms.assetid: 33e0f01e-39ac-46da-94ff-fe53b1116df4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e409d5064cb0e807d12a76b42055a6a43c9cb7c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948830"
---
# <a name="certprivatekey-transact-sql"></a>CERTPRIVATEKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Essa função retorna a chave privada de um certificado em formato binário. Essa função não utiliza três argumentos.
-   Uma ID de certificado.  
-   Uma senha de criptografia, usada para criptografar os bits de chave privada retornados pela função. Essa abordagem não expõe as chaves como um texto não criptografado para os usuários.  
-   Uma senha de descriptografia opcional. Uma senha de descriptografia especificada é usada para descriptografar a chave privada do certificado. Caso contrário, a chave mestra de banco de dados é usada.  
  
Somente os usuários com acesso à chave privada do certificado podem usar essa função. Essa função retorna a chave privada em formato PVK.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CERTPRIVATEKEY   
    (  
          cert_ID   
        , ' encryption_password '   
      [ , ' decryption_password ' ]  
    )  
```  
  
## <a name="arguments"></a>Argumentos  
*certificate_ID*  
A **certificate_id** do certificado. Obtenha esse valor de sys.certificates ou da função [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md). *cert_id* tem um tipo de dados **int**.
  
*encryption_password*  
A senha usada para criptografar o valor binário retornado.
  
*decryption_password*  
A senha usada para descriptografar o valor binário retornado.
  
## <a name="return-types"></a>Tipos de retorno
**varbinary**
  
## <a name="remarks"></a>Remarks  
Use **CERTENCODED** e **CERTPRIVATEKEY** em conjunto para retornar diferentes partes de um certificado em formato binário.
  
## <a name="permissions"></a>Permissões  
**CERTPRIVATEKEY** está disponível publicamente.
  
## <a name="examples"></a>Exemplos  
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Use 5tr0ng P^55Words'  
GO  
CREATE CERTIFICATE Shipping04   
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20401031';  
GO  
SELECT CERTPRIVATEKEY(CERT_ID('Shipping04'), 'jklalkaa/; uia3dd');  
```  
  
Consulte o Exemplo B em [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md) para obter um exemplo mais complexo que usa **CERTPRIVATEKEY** e **CERTENCODED** para copiar um certificado para outro banco de dados.
  
## <a name="see-also"></a>Confira também
[Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)
[Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
