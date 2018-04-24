---
title: CRYPT_GEN_RANDOM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1742e0d609372fcb2ad17859b503185ba04075ad
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="cryptgenrandom-transact-sql"></a>CRYPT_GEN_RANDOM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um número aleatório criptográfico gerado pela API de criptografia (CAPI). A saída é um número hexadecimal do número de bytes especificado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>Argumentos  
*length*  
O comprimento do número que está sendo criado. O máximo é 8000. *length* é do tipo **int**.
  
*seed*  
Dados opcionais a serem usados como semente aleatória.  Deve haver pelo menos *length* bytes de dados. *seed* é **varbinary(8000)**.
  
## <a name="returned-types"></a>Tipos retornados  
**varbinary(8000)**
  
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
  
## <a name="see-also"></a>Confira também
[RAND &#40;Transact-SQL&#41;](../../t-sql/functions/rand-transact-sql.md)
  
  
