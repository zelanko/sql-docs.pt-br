---
title: MakeValid (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MakeValid
- MakeValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid (geometry Data Type)
ms.assetid: 38673010-ab77-4ebb-9c4d-b26b79e3b7ea
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9c613a95ea3bee42d51ac1805ff65281fa96ec33
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101196"
---
# <a name="makevalid-geometry-data-type"></a>MakeValid (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Converte uma instância de **geometry** inválida em uma instância de **geometry** com um tipo válido do OGC (Open Geospatial Consortium).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Esse método causa uma alteração no tipo de instância de **geometry** e faz com que os pontos de uma instância de **geometry** sejam um pouco deslocados.  
  
## <a name="examples"></a>Exemplos  
 O primeiro exemplo cria uma instância inválida de `LineString` que se sobrepõe e usa `STIsValid()` para confirmar que é uma instância inválida. `STIsValid()` retorna o valor 0 para uma instância inválida.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 0);  
SELECT @g.STIsValid();  
```  
  
 O segundo exemplo usa `MakeValid()` pata tornar a instância válida e testar se ela é realmente válida. `STIsValid()` retorna o valor 1 para uma instância válida.  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.STIsValid();  
```  
  
 O terceiro exemplo verifica como a instância foi alterada para se tornar uma instância válida.  
  
```  
SELECT @g.ToString();  
```  
  
 Neste exemplo, quando a instância de `LineString` é selecionada, os valores são retornados como uma instância de `MultiLineString` válida.  
  
```  
MULTILINESTRING ((0 2, 1 1, 2 2), (1 1, 1 0))  
```  
  
 O exemplo a seguir converte a instância de CircularString em uma instância de Ponto.  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 1 1, 1 1)';  
SELECT @g.MakeValid().ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [STIsValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

