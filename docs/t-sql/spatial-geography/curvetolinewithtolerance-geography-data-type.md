---
title: CurveToLineWithTolerance (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CurveToLineWithTolerance_TSQL
- CurveToLineWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- CurveToLineWithTolerance method (geography)
ms.assetid: 74369c76-2cf6-42ae-b9cc-e7a051db2767
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6f81b5ba7ba6de057dd82090775013db55e4275b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68066487"
---
# <a name="curvetolinewithtolerance-geography-data-type"></a>CurveToLineWithTolerance (tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna uma aproximação poligonal de uma instância de **geography** que contém segmentos de arco circulares.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.CurveToLineWithTolerance( tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
_tolerance_  
É uma expressão **double** que define o erro máximo entre o segmento de arco circular original e sua aproximação linear.  
  
_relative_  
É uma expressão **bool** que indica se um máximo relativo para o desvio deve ser usado. Se o relativo for definido como falso (0), um máximo absoluto será definido para o desvio que um aproximado linear poderá ter. Quando o relativo for verdadeiro (1), a tolerância será calculada como um produto do parâmetro de tolerância e do diâmetro da caixa delimitadora do objeto espacial.  
  
## <a name="return-types"></a>Tipos de retorno  
Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
A definição de tolerância <= 0 gera uma exceção **ArgumentOutOfRange**.  
  
## <a name="remarks"></a>Comentários  
Esse método permite uma quantidade de tolerância de erro a ser especificada para a **LineString** resultante.  
  
O método **CurveToLineWithTolerance** retornará uma instância de **LineString** para uma instância de **CircularString** ou de **CompoundCurve** e uma instância de  **Polígono** para uma instância de **CurvePolygon**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>a. Usando valores de tolerância diferentes em uma instância de CircularString  
O seguinte exemplo mostra como a definição da tolerância afeta a instância de `LineString` retornada de uma instância de `CircularString`:  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. Usando o método em uma instância de MultiLineString que contém uma LineString  
O exemplo a seguir mostra o que é retornado de uma instância de `MultiLineString` que só contém uma instância de `LineString`:  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649))');  
SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. Usando o método em uma instância de MultiLineString que contém várias LineStrings  
O exemplo a seguir mostra o que é retornado de uma instância de `MultiLineString` que contém mais de uma instância `LineString`:  
  
```
DECLARE @g geography;  
SET @g = geography::Parse('MULTILINESTRING((-122.358 47.653, -122.348 47.649),(-123.358 47.653, -123.348 47.649))');  
SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. Definindo o relativo como true para uma instância de CurvePolygon de invocação  
O exemplo a seguir usa uma instância de `CurvePolygon` para chamar `CurveToLineWithTolerance()` com *relativo* definido como true:  
  
```
DECLARE @g geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658), (-122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
```  
  
## <a name="see-also"></a>Consulte Também  
[Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
