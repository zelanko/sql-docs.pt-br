---
title: HasM (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 05/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HasM_TSQL
- HasM
dev_langs:
- TSQL
helpviewer_keywords:
- HasM geography
ms.assetid: e752e97f-1619-437d-b962-48c188b4e94c
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 71e9abf7fa2bd8f313dc913b995e21a7cf01befb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="hasm-geography-data-type"></a>HasM (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna 1 (true) se pelo menos um objeto espacial contiver pelo menos um valor M; caso contrário, retorna 0 (false).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.HasM  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **booliano**  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
  
```tsql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)  
  
  

