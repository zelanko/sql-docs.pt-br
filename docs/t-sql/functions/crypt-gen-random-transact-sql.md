---
title: CRYPT_GEN_RANDOM (Transact-SQL) | Microsoft Docs
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
- CRYPT_GEN_RANDOM_TSQL
- CRYPT_GEN_RANDOM
dev_langs:
- TSQL
helpviewer_keywords:
- CRYPT_GEN_RANDOM function
ms.assetid: b74bd9d4-758e-4b94-89a0-76dcda6d8c42
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f2732196567dc98dc768e81b305ffa72ed453a94
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="cryptgenrandom-transact-sql"></a>CRYPT_GEN_RANDOM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um número aleatório criptográfico gerado pela API de criptografia (CAPI). A saída é um número hexadecimal do número de bytes especificado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>Argumentos  
*length*  
O comprimento do número que está sendo criado. O máximo é 8000. *comprimento* é do tipo **int**.
  
*semente*  
Dados opcionais a serem usados como semente aleatória.  Deve haver pelo menos *comprimento* bytes de dados. *semente* é **varbinary (8000)**.
  
## <a name="returned-types"></a>Tipos retornados  
**varbinary (8000)**
  
## <a name="permissions"></a>Permissões  
Esta função é pública e não requer permissões especiais.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-generating-a-random-number"></a>A. Gerando um número aleatório  
O exemplo a seguir gera um número aleatório de 50 bytes.
  
```sql
SELECT CRYPT_GEN_RANDOM(50) ;  
```  
  
O exemplo a seguir gera um número aleatório de 4 bytes usando uma semente de 4 bytes.
  
```sql
SELECT CRYPT_GEN_RANDOM(4, 0x25F18060) ;  
```  
  
## <a name="see-also"></a>Consulte também
[RAND &#40; Transact-SQL &#41;](../../t-sql/functions/rand-transact-sql.md)
  
  

