---
title: ASYMKEYPROPERTY (Transact-SQL) | Microsoft Docs
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
- ASYMKEYPROPERTY_TSQL
- ASYMKEYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASYMKEYPROPERTY
ms.assetid: a30581f2-e1b1-4996-93e6-527ff96b7c42
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62ed19d07264d971045582c093a4c5ccdf6d8926
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="asymkeyproperty-transact-sql"></a>ASYMKEYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna as propriedades de uma chave assimétrica.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ASYMKEYPROPERTY (Key_ID , 'algorithm_desc' | 'string_sid' | 'sid')  
```  
  
## <a name="arguments"></a>Argumentos  
*Key_ID*  
É o parâmetro Key_ID de uma chave assimétrica do banco de dados. Para localizar a Key_ID quando você souber apenas o nome da chave, use ASYMKEY_ID. *Key_ID* é o tipo de dados **int**.
  
**'**algorithm_desc**'**  
Especifica que a saída retorna a descrição do algoritmo da chave assimétrica. Disponível somente para chaves assimétricas criadas de um módulo EKM.
  
**'**string_sid**'**  
Especifica que a saída retorna o SID da chave assimétrica em **nvarchar()** formato.
  
**'**sid**'**  
Especifica que a saída retorna o SID da chave assimétrica em formato binário.
  
## <a name="return-types"></a>Tipos de retorno  
**sql_variant**
  
## <a name="permissions"></a>Permissões  
Requer algumas permissões na chave assimétrica e que a permissão VIEW não tenha sido negada para o chamador na chave assimétrica.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna as propriedades da chave assimétrica com Key_ID 256.
  
```sql
SELECT   
ASYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm,  
ASYMKEYPROPERTY(256, 'string_sid') AS String_SID,  
ASYMKEYPROPERTY(256, 'sid') AS SID ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[ALTER ASYMMETRIC KEY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
[REMOVER a chave ASSIMÉTRICA &#40; Transact-SQL &#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)  
[VERIFYSIGNEDBYASYMKEY &#40; Transact-SQL &#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)  
[Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[asymmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)  
[Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
[ASYMKEY_ID &#40; Transact-SQL &#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
[SYMKEYPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/symkeyproperty-transact-sql.md)
  
  

