---
title: fn_check_object_signatures (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_check_object_signatures_TSQL
- fn_check_object_signatures_TSQL
- fn_check_object_signatures
- sys.fn_check_object_signatures
dev_langs: TSQL
helpviewer_keywords: sys.fn_check_object_signatures function
ms.assetid: 47509566-d3d7-46a9-89c1-91b4895d56b9
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b4f237723380c7220086f4b6642609f6e9177315
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysfncheckobjectsignatures-transact-sql"></a>sys.fn_check_object_signatures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Retorna uma lista de todos os objetos assináveis e indica se um objeto foi assinado por um determinado certificado ou chave assimétrica. Se o objeto foi assinado pelo certificado ou pela chave assimétrica especificada, também indicará se a assinatura do objeto é válida.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_ check_object_signatures (   
    { '@class' } , { @thumbprint }   
  )   
```  
  
## <a name="arguments"></a>Argumentos  
 {' @*classe*'}  
 Identifica o tipo da impressão digital fornecida:  
  
-   'certificado'  
  
-   'chave assimétrica'  
  
 @*classe* é **sysname**.  
  
 {@*impressão digital* }  
 O hash SHA-1 do certificado com o qual a chave é criptografada, ou o GUID da chave assimétrica com a qual a chave é criptografada. @*impressão digital* é **varbinary(20)**.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 A tabela a seguir lista as colunas que **fn_check_object_signatures** retorna.  
  
|Coluna|Tipo|Description|  
|------------|----------|-----------------|  
|Tipo|**nvarchar(120)**|Retorna a descrição do tipo ou o assembly.|  
|entity_id|**int**|Retorna a id de objeto do objeto que está sendo avaliado.|  
|is_signed|**int**|Retorna 0 quando o objeto não foi assinado pela impressão digital fornecida. Retorna 1 quando o objeto foi assinado pela impressão digital fornecida.|  
|is_signature_valid|**int**|Quando o valor de is_signed é 1, retorna 0 quando a assinatura não é válida. Retorna 1 quando a assinatura é válida.<br /><br /> Quando o valor de is_signed é 0, sempre retorna 0.|  
  
## <a name="remarks"></a>Comentários  
 Use **fn_check_object_signatures** para confirmar que usuários mal-intencionados não violaram objetos.  
  
## <a name="permissions"></a>Permissões  
 Requer VIEW DEFINITION no certificado ou na chave assimétrica.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir detecta o certificado autenticado de esquema relativo ao banco de dados `master` e retorna o valor `is_signed` de 1 e o valor `is_signature_valid` de 1 para objetos que foram assinados pelo certificado autenticado de esquema e que têm assinaturas válidas.  
  
```  
USE master;  
-- Declare a variable to hold the thumbprint.  
DECLARE @thumbprint varbinary(20) ;  
-- Populate the thumbprint variable with the master database schema signing certificate.  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%' ;  
-- Evaluates the objects signed by the schema signing certificate  
SELECT type, entity_id, OBJECT_NAME(entity_id) AS [object name], is_signed, is_signature_valid  
FROM sys.fn_check_object_signatures ('certificate', @thumbprint) ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [IS_OBJECTSIGNED &#40; Transact-SQL &#41;](../../t-sql/functions/is-objectsigned-transact-sql.md)  
  
  
