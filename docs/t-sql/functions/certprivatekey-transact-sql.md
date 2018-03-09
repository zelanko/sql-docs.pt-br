---
title: CERTPRIVATEKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTPRIVATEKEY
- CERTPRIVATEKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTPRIVATEKEY
ms.assetid: 33e0f01e-39ac-46da-94ff-fe53b1116df4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: df513e6ce63ff49e31ad05e5a4dca0372de69c83
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="certprivatekey-transact-sql"></a>CERTPRIVATEKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna a chave privada de um certificado em formato binário. Essa função não utiliza três argumentos.
-   Uma ID de certificado.  
-   Uma senha de criptografia que é usada para criptografar os bits da chave privada quando são retornados pela função, para que as chaves não exponham texto não criptografado para os usuários.  
-   Uma senha de descriptografia que é opcional. Se uma senha de descriptografia for especificada, ela será usada para descriptografar a chave privada do certificado, caso contrário, será usada a chave mestra do banco de dados.  
  
Apenas usuários que têm acesso à chave privada do certificado poderão usar essa função. Essa função retorna a chave privada em formato PVK.
  
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
É o **certificate_id** do certificado. Isso está disponível de Certificates ou usando o [CERT_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/cert-id-transact-sql.md) função. *Cert_ID* é do tipo **int**
  
*encryption_password*  
A senha usada para criptografar o valor binário retornado.
  
*decryption_password*  
A senha usada para descriptografar o valor binário retornado.
  
## <a name="return-types"></a>Tipos de retorno
**varbinary**
  
## <a name="remarks"></a>Comentários  
**CERTENCODED** e **CERTPRIVATEKEY** são usados juntos para retornar diferentes partes de um certificado em formato binário.
  
## <a name="permissions"></a>Permissões  
**CERTPRIVATEKEY** está disponível para o público.
  
## <a name="examples"></a>Exemplos  
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Use 5tr0ng P^55Words'  
GO  
CREATE CERTIFICATE Shipping04   
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20141031';  
GO  
SELECT CERTPRIVATEKEY(CERT_ID('Shipping04'), 'jklalkaa/; uia3dd');  
```  
  
Para obter um exemplo mais complexo que usa **CERTPRIVATEKEY** e **CERTENCODED** para copiar um certificado para outro banco de dados, consulte o exemplo B no tópico [CERTENCODED &#40; Transact-SQL &#41; ](../../t-sql/functions/certencoded-transact-sql.md).
  
## <a name="see-also"></a>Consulte também
[Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[Criar certificado &#40; Transact-SQL &#41; ](../../t-sql/statements/create-certificate-transact-sql.md) 
 [Funções de segurança &#40; Transact-SQL &#41; ](../../t-sql/functions/security-functions-transact-sql.md) 
 [Certificates &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
