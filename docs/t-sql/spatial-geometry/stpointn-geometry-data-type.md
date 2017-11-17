---
title: STPointN (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d6e46115d41a0a1b717502ed8475884268ea1af0
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stpointn-geometry-data-type"></a>STPointN (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um ponto especificado em uma **geometria** instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É um **int** expressão entre 1 e o número de pontos de **geometria** instância.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
 Abra o tipo Geospatial Consortium (OGC): **ponto**  
  
## <a name="remarks"></a>Comentários  
 Se um **geometria** instância é criado, `STPointN()` retorna o ponto especificado por *expressão* ordenando os pontos na ordem em que eles foram originalmente de entrada.  
  
 Se um **geometria** instância foi criada pelo sistema, `STPointN()` retorna o ponto especificado por *expressão* ordenando todos os pontos na mesma ordem, eles seriam saída: primeiro por geometria, em seguida, pelo anel na geometria (se apropriado) e, em seguida, pelo ponto dentro do anel. Essa ordem é determinística.  
  
 Se esse método for chamado com um valor menor que 1, ele lança uma **ArgumentOutOfRangeException**.  
  
 Se esse método for chamado com um valor maior que o número de pontos na instância, retornará nulo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `STPointN()` para recuperar o segundo o ponto na descrição da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


