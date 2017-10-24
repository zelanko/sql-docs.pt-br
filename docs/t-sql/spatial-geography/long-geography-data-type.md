---
title: Long (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs:
- TSQL
helpviewer_keywords:
- Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0c69ce921e8aa22d65011a56d47c5cd7b05ad76f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="long-geography-data-type"></a>Long (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  A propriedade de longitude do **geografia** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Long  
```  
  
## <a name="return-value"></a>Valor de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 No modelo OpenGIS, tempo só é definido em **geografia** instâncias composto de um único ponto. Essa propriedade retornará NULL se **geografia** instâncias contêm mais de um único ponto. Essa propriedade é exata e somente leitura.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo cria um **ponto** instância e recupera a longitude do ponto.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

