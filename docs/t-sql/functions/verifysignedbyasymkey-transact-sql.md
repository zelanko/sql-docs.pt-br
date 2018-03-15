---
title: VERIFYSIGNEDBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- VERIFYSIGNEDBYASYMKEY_TSQL
- VERIFYSIGNEDBYASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- verifying digitally signed data for changes
- VERIFYSIGNEDBYASYMKEY
- testing digitally signed data for changes
- checking digitally signed data for changes
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 9f7c6e0b-5ba4-4dbb-994d-5bd59f4908de
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88e18f3f2eee5d77e450f7529336cc134f52ed44
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="verifysignedbyasymkey-transact-sql"></a>VERIFYSIGNEDBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Testa se dados assinados digitalmente foram alterados desde que foram assinados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
VerifySignedByAsymKey( Asym_Key_ID , clear_text , signature )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Asym_Key_ID*  
 É a ID de um certificado de chave assimétrica no banco de dados.  
  
 *clear_text*  
 São dados de texto não criptografado que estão sendo verificados.  
  
 *signature*  
 É a assinatura que foi anexada aos dados assinados. *assinatura* é **varbinary**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
 Retorna 1 quando as assinaturas forem correspondentes; caso contrário, retorna 0.  
  
## <a name="remarks"></a>Remarks  
 **VerifySignedByAsymKey** descriptografa a assinatura dos dados usando a chave pública da chave assimétrica especificada e compara o valor descriptografado a um hash de MD5 dos dados computados recentemente. Se os valores corresponderem, a assinatura será confirmada como válida.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DEFINITION na chave assimétrica.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-testing-for-data-with-a-valid-signature"></a>A. Testando se os dados têm uma assinatura válida  
 O exemplo a seguir retornará 1 se os dados selecionados não foram alterados desde a assinatura com a chave assimétrica `WillisKey74`. O exemplo retornará 0 se os dados foram violados.  
  
```  
SELECT Data,  
     VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), SignedData,  
     DataSignature ) as IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
RETURN;  
```  
  
### <a name="b-returning-a-result-set-that-contains-data-with-a-valid-signature"></a>B. Retornando um conjunto de resultados contendo dados com uma assinatura válida  
 O exemplo a seguir retorna linhas em `SignedData04` contendo dados que não foram alterados desde a assinatura com a chave assimétrica `WillisKey74`. O exemplo chama a função `AsymKey_ID` para obter a ID de chave assimétrica do banco de dados.  
  
```  
SELECT Data   
FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), Data,  
     DataSignature ) = 1  
AND Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
