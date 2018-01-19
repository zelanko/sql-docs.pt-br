---
title: STEquals (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STEquals (geometry Data Type)
- STEquals_TSQL
dev_langs: TSQL
helpviewer_keywords: STEquals (geometry Data Type)
ms.assetid: 808f0e25-9e68-4ba7-9329-07ec950698f3
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e964ddf7cca192d758d9da4891fa6b6729d64a9c
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="stequals-geometry-data-type"></a>STEquals (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retornará 1 se uma **geometria** instância representa o mesmo ponto definido como outro **geometria** instância. Retornará 0 se isso não ocorrer.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STEquals ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 É outra **geometria** instância a ser comparada com a instância na qual `STEquals()` é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 Esse método sempre retornará nulo se as IDs de referência espaciais (SRIDs) da **geometria** instâncias não coincidem.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria dois `geometry` instâncias com `STGeomFromText()` que são iguais, mas não superficialmente iguais e usa `STEquals()` para testar sua igualdade.  
  
```  
DECLARE @g geometry  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('MULTILINESTRING((4 2, 2 0), (0 2, 2 0))', 0);  
SELECT @g.STEquals(@h);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

