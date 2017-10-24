---
title: "HasM (DataType Geométrico) | Microsoft Docs"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- HasM geometry
ms.assetid: 15540837-c4bf-4d18-b380-13ae31f3226f
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5086605b21d8ad5df273c67bf5737b9fb4279673
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="hasm-geometry-datatype"></a>HasM (DataType geométrico)
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
DECLARE @p GEOMETRY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)  
  
  

