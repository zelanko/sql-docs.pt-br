---
title: VERIFYSIGNEDBYCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VERIFYSIGNEDBYCERT
- VERIFYSIGNEDBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- digitally signed data for changes [SQL Server]
- verifying digitally signed data for changes
- testing digitally signed data for changes
- checking digitally signed data for changes
- VERIFYSIGNEDBYCERT
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 4e041f33-60c4-4190-91c7-220d51dd6c8f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 360b597b8cd122ede57426cc879dd041b3414078
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67927552"
---
# <a name="verifysignedbycert-transact-sql"></a>VERIFYSIGNEDBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Testa se dados assinados digitalmente foram alterados desde que foram assinados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
VerifySignedByCert( Cert_ID , signed_data , signature )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cert_ID*  
 É a ID de um certificado no banco de dados. *Cert_ID* é **int**.  
  
 *signed_data*  
 É uma variável do tipo **nvarchar**, **char**, **varchar** ou **nchar** que contém dados que foi assinados com um certificado.  
  
 *signature*  
 É a assinatura que foi anexada aos dados assinados. *assinatura* é **varbinary**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
 Retorna 1 quando os dados assinados estão inalterados, caso contrário, retorna 0.  
  
## <a name="remarks"></a>Comentários  
 **VerifySignedBycert** descriptografa a assinatura dos dados usando a chave pública da chave assimétrica especificada e compara o valor descriptografado a um hash de MD5 dos dados computados recentemente. Se os valores corresponderem, a assinatura será confirmada como válida.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão VIEW DEFINITION no certificado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-verifying-that-signed-data-has-not-been-tampered-with"></a>a. Verificando se os dados assinados não foram violados  
 O exemplo a seguir testa se as informações em `Signed_Data` foram alteradas desde que foram assinadas com o certificado chamado `Shipping04`. A assinatura é armazenada em `DataSignature`. O certificado, `Shipping04`, é passado para `Cert_ID`, que retorna a ID do certificado no banco de dados. Se `VerifySignedByCert` retornar 1, a assinatura estará correta. Se `VerifySignedByCert` retornar 0, os dados em `Signed_Data` não serão os que foram usados para gerar `DataSignature`. Neste caso, ou `Signed_Data` foi alterado desde que foi assinado ou `Signed_Data` foi assinado com um certificado diferente.  
  
```  
SELECT Data, VerifySignedByCert( Cert_Id( 'Shipping04' ),  
    Signed_Data, DataSignature ) AS IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
### <a name="b-returning-only-records-that-have-a-valid-signature"></a>B. Retornando somente registros que tenham uma assinatura válida  
 Esta consulta retorna somente os registros que não foram alterados desde que foram assinados com o certificado `Shipping04`.  
  
```  
SELECT Data FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByCert( Cert_Id( 'Shipping04' ), Data,   
    DataSignature ) = 1   
AND Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [SIGNBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/signbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
