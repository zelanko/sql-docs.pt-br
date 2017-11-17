---
title: CERTPROPERTY (Transact-SQL) | Microsoft Docs
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
- CERTPROPERTY
- CERTPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], schema names
- schemas [SQL Server], names
- CERTPROPERTY function
ms.assetid: 966c09aa-bc4e-45b0-ba53-c8381871f638
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b43b587688b574c6d6395b72c5b368b82e617fd
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="certproperty-transact-sql"></a>CERTPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o valor de uma propriedade de certificado especificada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CertProperty ( Cert_ID , '<PropertyName>' )  
  
<PropertyName> ::=  
   Expiry_Date | Start_Date | Issuer_Name   
   | Cert_Serial_Number | Subject | SID | String_SID   
```  
  
## <a name="arguments"></a>Argumentos  
*Cert_ID*  
É a ID do certificado. *Cert_ID* é int.
  
*Expiry_Date*  
É a data de expiração do certificado.
  
*Start_Date*  
É a data em que o certificado se torna válido.
  
*Issuer_Name*  
É o nome do emissor do certificado.
  
*Cert_Serial_Number*  
É o número de série do certificado.
  
*Assunto*  
É o assunto do certificado.
  
 *SID*  
É o SID do certificado. Também é o SID de qualquer logon ou usuário mapeado para esse certificado.
  
*String_SID*  
É o SID do certificado como uma cadeia de caracteres. Também é o SID de qualquer logon ou usuário mapeado para o certificado.
  
## <a name="return-types"></a>Tipos de retorno
A especificação de propriedade deve ser incluída entre aspas simples.
  
O tipo de retorno depende da propriedade especificada na chamada de função. Todos retornam valores são encapsulados no tipo de retorno de **sql_variant**.
-   *Expiry_Date* e *Start_Date* retornar **datetime**.  
-   *Cert_Serial_Number*, *Issuer_Name*, *assunto*, e *String_SID* retornar **nvarchar**.  
-   *SID* retorna **varbinary**.  
  
## <a name="remarks"></a>Comentários  
Informações sobre certificados são visíveis no [Certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) exibição do catálogo.
  
## <a name="permissions"></a>Permissões  
Requer algumas permissões no certificado e que a permissão VIEW DEFINITION não seja negada ao chamador no certificado.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna o assunto do certificado.
  
```sql
-- First create a certificate.  
CREATE CERTIFICATE Marketing19 WITH   
    START_DATE = '04/04/2004' ,  
    EXPIRY_DATE = '07/07/2007' ,  
    SUBJECT = 'Marketing Print Division';  
GO  
  
-- Now use CertProperty to examine certificate  
-- Marketing19's properties.  
DECLARE @CertSubject sql_variant;  
set @CertSubject = CertProperty( Cert_ID('Marketing19'), 'Subject');  
PRINT CONVERT(nvarchar, @CertSubject);  
GO  
```  
  
## <a name="see-also"></a>Consulte também
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[ALTER CERTIFICATE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)  
[CERT_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/cert-id-transact-sql.md) 
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)
[Certificates &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 
 [Exibições do catálogo de segurança &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  

