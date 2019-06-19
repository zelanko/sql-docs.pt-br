---
title: CERTPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: c27111dac0da8d9248bea1b7d7408cd70130d01b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948802"
---
# <a name="certproperty-transact-sql"></a>CERTPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o valor de uma propriedade de certificado especificada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CertProperty ( Cert_ID , '<PropertyName>' )  
  
<PropertyName> ::=  
   Expiry_Date | Start_Date | Issuer_Name   
   | Cert_Serial_Number | Subject | SID | String_SID   
```  
  
## <a name="arguments"></a>Argumentos  
*Cert_ID*  
O valor da ID de certificado, do tipo de dados int.
  
*Expiry_Date*  
A data de expiração do certificado.
  
*Start_Date*  
A data em que o certificado se torna válido.
  
*Issuer_Name*  
O nome do emissor do certificado.
  
*Cert_Serial_Number*  
O número de série do certificado.
  
*Assunto*  
A entidade do certificado.
  
 *SID*  
O SID do certificado. Também é o SID de qualquer logon ou usuário mapeado para esse certificado.
  
*String_SID*  
O SID do certificado como uma cadeia de caracteres. Também é o SID de qualquer logon ou usuário mapeado para o certificado.
  
## <a name="return-types"></a>Tipos de retorno
Aspas simples devem incluir a especificação da propriedade.
  
O tipo de retorno depende da propriedade especificada na chamada de função. O tipo de retorno **sql_variant** encapsula todos os valores retornados.
-   *Expiry_Date* e *Start_Date* retornam **datetime**.  
-   *Cert_Serial_Number*, *Issuer_Name*, *String_SID* e *Subject* retornam **nvarchar**.  
-   *SID* retorna **varbinary**.  
  
## <a name="remarks"></a>Remarks  
Consulte as informações de certificado na exibição de catálogo [sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md).
  
## <a name="permissions"></a>Permissões  
Exige as permissões apropriadas no certificado e que a permissão VIEW não tenha sido negada ao chamador no certificado. Consulte [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md) e [GRANT CERTIFICATE PERMISSIONS &#40;Transact-SQL&#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md) para obter mais informações sobre permissões de certificado.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna o assunto do certificado.
  
```sql
-- First create a certificate.  
CREATE CERTIFICATE Marketing19 WITH   
    START_DATE = '04/04/2004' ,  
    EXPIRY_DATE = '07/07/2040' ,  
    SUBJECT = 'Marketing Print Division';  
GO  
  
-- Now use CertProperty to examine certificate  
-- Marketing19's properties.  
DECLARE @CertSubject sql_variant;  
set @CertSubject = CertProperty( Cert_ID('Marketing19'), 'Subject');  
PRINT CONVERT(nvarchar, @CertSubject);  
GO  
```  
  
## <a name="see-also"></a>Confira também
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)  
[CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)
[Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)
[Certificados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
[Exibições do catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  
